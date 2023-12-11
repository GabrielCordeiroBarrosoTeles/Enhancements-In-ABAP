# Enhancements-In-ABAP

Em SAP ABAP, os Enhancements (aperfeiçoamentos ou melhorias) são mecanismos que permitem adicionar, modificar ou substituir código em programas padrão sem modificar diretamente o código fonte original. Isso é feito para estender a funcionalidade padrão do sistema sem interferir nos objetos originais.

Existem dois tipos principais de Enhancements no SAP ABAP: Implicit Enhancements e Explicit Enhancements.

### Implicit Enhancements:

Os aperfeiçoamentos implícitos são pontos de extensão no código padrão onde você pode adicionar código sem modificar o código original. Eles são implementados usando o conceito de `ENHANCEMENT-POINT` e `ENHANCE` no código ABAP.

**Exemplo:**

Considere uma função padrão do SAP que retorna o dobro de um número:

```abap
FUNCTION Z_DOUBLE_NUMBER.
  IMPORTING
    VALUE(iv_number) TYPE i
  EXPORTING
    VALUE(ev_result) TYPE i.

  ev_result = 2 * iv_number.
ENDFUNCTION.
```

Agora, você deseja adicionar uma verificação adicional ao número antes de calcular o dobro. Você pode usar um aperfeiçoamento implícito para fazer isso:

```abap
FUNCTION Z_DOUBLE_NUMBER.
  IMPORTING
    VALUE(iv_number) TYPE i
  EXPORTING
    VALUE(ev_result) TYPE i.

  " Enhancements
  ENHANCEMENT-POINT IMP_POINT.

  ev_result = 2 * iv_number.
ENDFUNCTION.

" Enhancements Implementation
ENHANCEMENT 1 Z_DOUBLE_NUMBER.
  " Seu código adicional aqui
  IF iv_number > 10.
    ev_result = 0. " Zera o resultado se o número for maior que 10
  ENDIF.
ENDENHANCEMENT.
```

### Explicit Enhancements:

Os aperfeiçoamentos explícitos são áreas específicas no código padrão onde você pode adicionar código usando a palavra-chave `ENHANCEMENT` diretamente no código fonte original.

**Exemplo:**

Considere uma classe padrão do SAP com um método:

```abap
CLASS zcl_example DEFINITION.
  PUBLIC SECTION.
    METHODS: calculate_sum
             IMPORTING
               iv_number1 TYPE i
               iv_number2 TYPE i
             RETURNING
               VALUE(rv_sum) TYPE i.
ENDCLASS.

CLASS zcl_example IMPLEMENTATION.
  METHOD calculate_sum.
    rv_sum = iv_number1 + iv_number2.
  ENDMETHOD.
ENDCLASS.
```

Agora, suponha que você queira adicionar uma verificação adicional ao resultado. Você pode usar um aperfeiçoamento explícito para fazer isso:

```abap
CLASS zcl_example DEFINITION.
  PUBLIC SECTION.
    METHODS: calculate_sum
             IMPORTING
               iv_number1 TYPE i
               iv_number2 TYPE i
             RETURNING
               VALUE(rv_sum) TYPE i.
ENDCLASS.

CLASS zcl_example IMPLEMENTATION.
  METHOD calculate_sum.
    rv_sum = iv_number1 + iv_number2.

    " Enhancement
    ENHANCEMENT 1 ZCL_EXAMPLE.

    " Seu código adicional aqui
    IF rv_sum > 100.
      rv_sum = 100. " Limita o resultado a 100
    ENDIF.
  ENDMETHOD.
ENDCLASS.
```

Esses são exemplos básicos de como usar Enhancements no SAP ABAP para estender a funcionalidade de programas padrão sem modificar diretamente o código fonte original.
