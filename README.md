# brasil_fields

O jeito mais fácil de utilizar padrões e formatos brasileiros em seu projeto.

## Apresentação

Este package facilita o desenvolvimento com a linguagem Dart em projetos que
utilizam campos com os padrões e formatos brasileiros.

### Instalação

```yaml
dependencies:
  brasil_fields: ^0.6.0
```

### Formatters

- Altura (2,22)
- Cartão bancário (0000 1111 2222 3333 4444)
- CEP (99.999-999)
- CNPJ (99.999.999/9999-99)
- CPF (999.999.99-99)
- Cpf ou Cnpj (se adapta conforme os números são inseridos)
- Data (01/01/1900)
- Hora (23:59)
- KM (999.999)
- Peso (111,1)
- Real (R\$) (20.550)
- Telefone ( (99) 9999-9999)
- Validade de cartão bancário (12/24)


![Formatters](screenshots/formatters.png)

### Padrões

- Estados
- Meses
- Regiões
- Semana

![Formatters](screenshots/padroes.png)

### Como utilizar

Basta incluir o formatter que você quer que o campo tenha, na lista de `inputFormatters` :

**Para garantir que o campo aceite apenas valores numéricos, utilize em conjunto com o formatter `FilteringTextInputFormatter.digitsOnly` .**

```dart
TextFormField(
  inputFormatters: [
    FilteringTextInputFormatter.digitsOnly,
    CepInputFormatter(),
  ],
);
```

- `AlturaInputFormatter()`
- `CartaoBancarioInputFormatter()`
- `CepInputFormatter()`
- `CnpjInputFormatter()`
- `CpfInputFormatter()`
- `CpfOuCnpjFormatter()`
- `DataInputFormatter()`
- `HoraInputFormatter()`
- `KmInputFormatter()`
- `PesoInputFormatter()`
- `RealInputFormatter()`
- `TelefoneInputFormatter()`
- `ValidadeCartaoInputFormatter()`

Caso precise de um DropdownButton com algumas das classes de padrões:

```dart
DropdownButton(
  items: Regioes.listaRegioes.map((String opcao) {
    return DropdownMenuItem<String>(
    value: opcao,
    child: Text(opcao),
  );
}).toList(),
```

### Métodos úteis

A classe `UtilData` possui métodos que facilitam obter o valor de um objeto `DateTime` em formato `String` (e no padrão brasileiro).

- `UtilData.obterDataDDMMAAAA` (DD/MM/AAAA)
- `UtilData.obterDataMMAAAA` (MM/AAAA)
- `UtilData.obterDataDDMM` (MM/AAAA)
- `UtilData.obterHoraHHMMSS` (hh:mm:ss)
- `UtilData.obterHoraHHMM` (hh:mm)

A classe `UtilBrasilFields` possui métodos que facilitam obtert os valores CEP, CPF e CPNJ já formatados:

- `UtilBrasilFields.obterCpf('11122233344')` (111.222.333-44)
- `UtilBrasilFields.obterCnpj('11222333444455')` (11.222.333/4444-55)
- `UtilBrasilFields.obterCep('11222333')` (11.222-333)
- `UtilBrasilFields.obterCep('11222333', ponto: false)` (11222-333)
- `UtilBrasilFields.obterTelefone('00999998877')` ((00) 99999-8877)
- `UtilBrasilFields.obterTelefone('999998877', ddd: false)` (99999-8877)

Para inicializar um `TextEditingController` com o texto já formatado, basta escolher o método com o formato desejado e setar no atributo `text`:

```dart
  final dataController = TextEditingController(text: UtilData.obterDataDDMMAAAA(DateTime(2020, 12, 31)));
  final cnpjController = TextEditingController(text: UtilBrasilFields.obterCnpj('11222333444455'));
```
