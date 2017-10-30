# Mini-C-compiler
Mini C compiler for programming assignment  
Dongguk University -  Computer Science & Engineering  
Compiler Construction - CSE4035, Seman Oh



## Mini C Grammar
```
DIRECTIVE       BUILD_TREES -> OFF;
                LIST_STATES -> ON;

LEXICON         '%IDENT' => IDENT;
                '%NUMBER' => NUMBER;

SYNTAX MINI_C

MINI_C        -> DCL MAIN_FUNC                               => PROGRAM;
DCL           -> FUNC_DCL VAR_DCL                            => DCL;
MAIN_FUNC     -> 'void' 'main' '(' ')' FUNC_BODY             => MAIN_FUNC;
FUNC_DCL      -> FUNC_DEFS                                   => FUNC_DCL;
              -> ;
FUNC_DEFS     -> FUNC_DEF;
              -> FUNC_DEFS FUNC_DEF;
FUNC_DEF      -> FUNC_HEAD FUNC_BODY                         => FUNC_DEF;
FUNC_HEAD     -> TYPE '%IDENT' OPT_FORM_PARAM;
OPT_FORM_PARAM-> '(' FORMAL_PARAMS ')'                       => FORM_PARAM;
FORMAL_PARAMS -> FORMAL_PARAM;
              -> FORMAL_PARAMS ',' FORMAL_PARAM;
FORMAL_PARAM  -> TYPE '%IDENT'                               => VALUE_PARAM;
              -> TYPE POINTER '%IDENT'                       => VAR_PARAM;
FUNC_BODY     -> '{' VAR_DCL STATEMENTS '}';
VAR_DCL       -> VAR_DEFS                                    => VAR_DCL;
              -> ;
VAR_DEFS      -> VAR_DEF;
              -> VAR_DEFS VAR_DEF;
VAR_DEF       -> TYPE VAR_LIST ';'                           => VAR_DEF;
VAR_LIST      -> IDENT_LIST                                  => VAR_LIST;
TYPE          -> '%IDENT'                                    => INT_VOID_TYPE;
IDENT_LIST    -> IDENTS;
              -> IDENT_LIST ',' IDENTS;
IDENTS        -> '%IDENT';
              -> '%IDENT' '[' '%NUMBER' ']'                  => ARRAY_VAR;
              -> POINTER '%IDENT'                            => POINTER_VAR;
STATEMENT     -> ASSIGNMENT_ST;
              -> EXPRESSION;
              -> COMPOUND_ST;
              -> IF_ST;
              -> SWITCH_ST;
              -> WHILE_ST;
              -> DO_WHILE_ST;
              -> FOR_ST;
              -> JUMP_ST;                        
              -> NULL_ST;
              -> ;
ASSIGNMENT_ST -> VARIABLE '=' EXP ';'                        => ASSIGN_STMT;
EXPRESSION    -> EXP ';'                                     => EXPRESSION;     
OPT_ACT_PARAM -> '(' ACTUAL_PARAMS ')'                       => ACTUAL_PARAM;
ACTUAL_PARAMS -> EXP;
              -> ACTUAL_PARAMS ',' EXP;
COMPOUND_ST   -> '{' STATEMENTS '}'                         => COMPOUND_STMT;
STATEMENTS    -> STATEMENT;
              -> STATEMENTS STATEMENT;
IF_ST         -> 'if' '(' CONDITION ')' STATEMENT           => IF_STMT;
              -> 'if' '(' CONDITION ')' STATEMENT 'else' STATEMENT => IF_ELSE_STMT;
SWITCH_ST     -> 'switch' '(' '%IDENT' ')' '{' CASE_LIST '}' => SWITCH_STMT;
CASE_LIST     -> CASE;
              -> CASE_LIST CASE;
CASE          -> 'case' '%NUMBER' ':' STATEMENT              => CASE;
              -> 'default' ':' STATEMENT                     => DEFAULT_CASE;
WHILE_ST      -> 'while' '(' CONDITION ')' STATEMENT         => WHILE_STMT;
DO_WHILE_ST   -> 'do' STATEMENT 'while' '(' CONDITION ')' STATEMENT => DO_WHILE_STMT;
FOR_ST        -> 'for' '(' ASSIGNMENT_ST ';' CONDITION ';' ASSIGNMENT_ST ')' STATEMENT => FOR_STMT;
JUMP_ST       -> 'break' ';'                                 => BREAK;
              -> 'continue' ';'                              => CONTINUE;
              -> 'return' OPT_EXP                            => RETURN;
NULL_ST       -> ';';
OPT_EXP       -> EXP;
              -> ;
CONDITION     -> EXP '==' EXP                                => EQ;
              -> EXP '!=' EXP                                => NE;
              -> EXP '>' EXP                                 => GT;
              -> EXP '>=' EXP                                => GE;
              -> EXP '<' EXP                                 => LT;
              -> EXP '<=' EXP                                => LE;
EXP           -> EXP '+' EXP                                 => ADD;
              -> EXP '-' EXP                                 => SUB;
              -> TERM;
TERM          -> TERM '*' FACTOR                             => MUL;
              -> TERM '/' FACTOR                             => DIV;
              -> TERM '%' FACTOR                             => MOD;
              -> FACTOR;
FACTOR        -> '!' FACTOR                                  => NEG;
              -> VARIABLE;
              -> '%NUMBER';
              -> '(' EXP ')';
VARIABLE      -> '%IDENT';
              -> '%IDENT' '[' EXP ']'                        => INDEX;
              -> POINTER '%IDENT'                            => POINTER;
              -> '&' '%IDENT'                                => REFERENCE;
              -> '%IDENT' OPT_ACT_PARAM                      => CALL_STMT;
POINTER       -> '*';
```
