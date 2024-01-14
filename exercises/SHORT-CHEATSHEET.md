# 1
- void createVariable
- int get_symbol_location
- void gen_addi_instruction
- void gen_addi_instruction(program , r_var , REG_0 , 42);
- void gen_read_instruction

# 2
- int getNewRegister
- void gen_move_immediate
- int gen_load_immediate
- void gen_slt_instruction
---
- t_axe_expression create_expression
- t_axe_expression handle_bin_numeric_op
---
- int loadArrayElement
- void storeArrayElement
- t_axe_variable getVariable

# 3
- t_axe_label* newLabel && void assignLabel
- t_axe_label* assignNewLabel
- void gen_bt_instruction