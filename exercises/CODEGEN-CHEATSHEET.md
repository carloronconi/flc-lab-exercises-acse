## Declaring a scalar/array variable

```
declaration : IDENTIFIER
    {
    extern void createVariable(t_program_infos *program, 
                               $1,              /* char *id */
                               INTEGER_TYPE,    /* int type */
                               0,               /* int isArray change to 1 if array */
                               0,               /* int arraySize change to $3 if array */
                               0);              /* int init_val change to $3 if assigned to value */
    }
```
## Storing value in scalar/MACE ADD
```
int r_var = get_symbol_location(program , "a", 0);
gen_addi_instruction(program , r_var , REG_0 , 42);
```
```
int r1 = get_symbol_location(program , "a", 0);
int r2 = get_symbol_location(program , "b", 0);
int r3 = get_symbol_location(program , "c", 0);
gen_add_instruction(program , r1, r2, r3, CG_DIRECT_ALL);
```
Other equivalents to add exist

## Reading from terminal to variable
```
read_statement : READ LPAR IDENTIFIER RPAR
                 {
                 int location;
                 location = get_symbol_location(program , $3, 0);
                 gen_read_instruction(program , location);
                 free($3);
                 }
```
## Getting an extra register (W/O FOLDING)
ASM often requires intermediate registers which don't correspond to actual LANCE variables (thus they are extra)
```
exp : NUMBER
    {
    $$ = getNewRegister(program);
    gen_addi_instruction(program , $$, REG_0 , $1);
    }
```
Shortcuts for storing immediate in preexisting/new register:
```
void gen_move_immediate(t_program_infos *program , int dest, int imm) {
    gen_addi_instruction(program , dest, REG_0 , imm);
}

int gen_load_immediate(t_program_infos *program , int imm) {
    int imm_register;
    imm_register = getNewRegister(program);
    gen_move_immediate(program , imm_register , imm);
    return imm_register;
}
```

## Constant folding: double meaning for semantic values of exp's
```
exp : /* ... */
{
    $$.expression_type = /* IMMEDIATE or REGISTER */
    $$.value = /* the constant or the register ident. */
}
```
Shortcut:
```
t_axe_expression create_expression(int value , int type) {
    t_axe_expression expression;
    expression.value = value;
    expression.expression_type = type;
    return expression;
}
```

## Corrected exp's with folding
```
exp : NUMBER
    {
        $$ = create_expression($1, IMMEDIATE);
    }
    | IDENTIFIER
    {
        int location = get_symbol_location(program , $1, 0);
        $$ = create_expression(location , REGISTER);
        free($1);
    }
    | LPAR exp RPAR
    {
        $$ = $2;
    }
```

## Codegen for operators: checking expression type
```
exp : exp PLUS exp
    {
        if ($1.expression_type==IMMEDIATE && $3.expression_type==IMMEDIATE)
        {
            $$ = create_expression($1.value + $3.value , IMMEDIATE);
        }
        else
        {
            int r1, r2, rres;
            if ($1.expression_type == IMMEDIATE)
                r1 = gen_load_immediate(program , $1.value);
            else
                r1 = $1.value;
            if ($3.expression_type == IMMEDIATE)
                r2 = gen_load_immediate(program , $3.value);
            else
                r2 = $3.value;
            rres = getNewRegister(program);
            gen_add_instruction(program , rres, r1, r2, CG_DIRECT_ALL);
            $$ = create_expression(rres, REGISTER);
        }
    }
```
Shortcut used for all binary operators:
```
t_axe_expression handle_bin_numeric_op(t_program_infos *program, t_axe_expression exp1, t_axe_expression exp2, int binop);
```

## Assigning variable or immediate to variable
```
assign_statement: IDENTIFIER ASSIGN exp
{
    int location;
    location = get_symbol_location(program , $1, 0);
    if ($3.expression_type == IMMEDIATE)
        gen_move_immediate(program , location , $3.value);
    else
        gen_add_instruction(program, location , REG_0 , $3.value , CG_DIRECT_ALL);
    free($1);
}
```

## The write statement
```
write_statement: WRITE LPAR exp RPAR
{
    int location;
    if ($3.expression_type == IMMEDIATE)
        location = gen_load_immediate(program , $3.value);
    else
        location = $3.value;
    gen_write_instruction(program , location);
}
```

## FMA cases example
Statement between identifiers
```

```
Statement between exp's
```

```
Operator
```

```