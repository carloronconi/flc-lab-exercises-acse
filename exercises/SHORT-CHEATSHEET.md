# lab-04-acse
- void createVariable(t_program_infos *program, char *ID, int type, int isArray, int arraySize, int init_val); // see lab-04-acse
- int get_symbol_location(t_program_infos *program, char *ID, int genLoad=0);
- void gen_add_instruction(program , r1, r2, r3, CG_DIRECT_ALL);
- void gen_addi_instruction(program , r_var , REG_0 , 42);
- void gen_read_instruction(program, int symbol_location)

# lab-05-acse
- int getNewRegister(t_program_infos *program);
- void gen_move_immediate(t_program_infos *program , int dest, int imm);
- int gen_load_immediate(t_program_infos *program , int imm);
- void gen_slt_instruction(program , label);
---
- t_axe_expression create_expression(int value , int type); // type is IMMEDIATE or REGISTER
- t_axe_expression handle_bin_numeric_op(t_program_infos *program, t_axe_expression exp1, t_axe_expression exp2, int binop); // Valid values for `binop`: ADD, SUB, MUL, DIV, SHL, SHR, ANDB, ANDL, ORB, ORL, EORB, EORL
---
- int loadArrayElement(t_program_infos *program, char *ID, t_axe_expression index);
- void storeArrayElement(t_program_infos *program, char *ID, t_axe_expression index, t_axe_expression data);
- t_axe_variable *getVariable(t_program_infos *program, char *ID); // typedef struct t_axe_variable { char *ID; int type; int isArray; int arraySize; int location; t_axe_label *labelID; } t_axe_variable;

# lab-06-acse
- t_axe_label* newLabel(program); void assignLabel(program, t_axe_label* label);
- t_axe_label* assignNewLabel(program);
- void gen_bt_instruction(program, label, 0);

# Landscape reference
- extern int loadArrayElement(t_program_infos *program, char *ID, t_axe_expression index);
- extern void storeArrayElement(t_program_infos *program, char *ID, t_axe_expression index, t_axe_expression data);

- extern t_axe_label *newLabel(t_program_infos *program);
- extern t_axe_label *assignLabel(t_program_infos *program, t_axe_label *label);
- extern t_axe_label *assignNewLabel(t_program_infos *program);

- extern void createVariable(t_program_infos *program, char *ID, int type, int isArray, int arraySize, int init_val);

- extern t_axe_variable *getVariable(t_program_infos *program, char *ID);
- extern int get_symbol_location(t_program_infos *program, char *ID, int genLoad=0);

- extern int getNewRegister(t_program_infos *program);
- extern int gen_load_immediate(t_program_infos *program, int immediate);
- extern void gen_move_immediate(t_program_infos *program, int dest, int imm);

- extern t_axe_expression create_expression(int value, int type);

- /* Valid values for `binop': ADD, SUB, MUL, DIV, SHL, SHR, ANDB, ANDL, ORB, ORL, EORB, EORL */
- extern t_axe_expression handle_bin_numeric_op(t_program_infos *program, t_axe_expression exp1, t_axe_expression exp2, int binop);
- 
- /* Valid values for `condition': _LT_, _GT_, _EQ_, _NOTEQ_, _LTEQ_, _GTEQ_ */
- extern t_axe_expression handle_binary_comparison(t_program_infos *program, t_axe_expression exp1, t_axe_expression exp2, int condition);