# BADE (to bid your data!)

Its an easy and lite jQuery JavaScript plugin to use within 
(Twitters) Bootstrap AdminLTE DataTable Editor. Its made to use
within AdminLTE Bootstrap template, but it should be instant ready
with eny template, specialy if you use font-awesome icon set.

## Getting Started

Just go! Its easy as clone the directory in your repo and start working.

## Instalation

create a directory wherever you wish in your project's structure and use the old and gold ...

```shell
git clone git@github.com:rstriquer/BADE.git .
```

## Initial Configuration

Well its not about configuration, the plugin have no actual configuration,
but bare in mind this is the very first zero version therefor (and as allways)
we had no time to implement translations for any other language but 
Portuguese-Brasil, so ... if you are fond of any other language we urge to you
to fork! Go around, make some changes and get back to us about translations
and stuff.

## How To Use

To use the plugin in you page you'd have to have ...

... a link to load the plugin in the HTML file

```html
<script type="text/javascript" src="/[path to ...]/jquery.BADU.js"></script>
```

... a table (and if you'd like a personalized external "add button" ...)
```html
<button type="button" class="btn btn-default" id="dt_user_add"><i class="fa fa-plus"></i></button> System Users:<br />
<table id="dt_user" class="table table-bordered table-hover"></table>
```

and finely the javascript code ...
```javascript
var users = {
	'title_new': 'Add new User to the Table!', 'title_old': 'Editing Users Data!', 'table_id': 'dt_users','fields': [
	{'label': 'Users contact email', 'title': 'Email', 'type': 'i', 'placeholder': 'A valid personal email.', 'required': 'You must provide an email.'},
	{'label': 'User Type', 'title': 'Type', 'type': 's', 'options': [
		{'label': 'Please Select', 'value': '', 'default': true}, {'label': 'Operator', 'value': 'operator'}, {'label': 'Administrator', 'value': 'admin'},
	], 'required': 'You must choose the users type'}
	],
};
jQuery.fn.CreateDataTableLite(users);
```

## Parameters

For a better understanding of the project please visit the [Projct Wiki in github]{https://github.com/rstriquer/BADE).
Bellow a simple reference to easy the day-to-day use.

```javascript
var users = {
  // A forms title line to use whenever its an add action
  'title_new': 'Adding a New Line', 
  // A form's title line to use whenever its an update action
  'title_old': 'Updating an existent line!',
  // the table's id to bind the form to
  'table_id': 'dt_emails',
  // fields configurations
  'fields': [
    {
      // label of the form field to show to the user
      'label': 'Name of the user',
      // table title.
      'title': 'Name',
      // input form placeholder, used for input and text fields only
      // - ignored when using mask parameter or in a 'img' field type
      'placeholder': null,
      // default value fot input field
      // - if its a 'ck' (checkbox) field type them it shoud be 
      //   true (as in selected) or false (as in not selected) or 
      //   even not be created, which is the same as false.
      'default': null,
      // when updating we use this field. Its more of an intern field
      'value': null,
      // type, should be 
      //  i) Input;
      //  t) textfield;
      // ck) Checkbox;
      //  s) Select field;
      //  r) Radio button;
      'type': 's',
      // area para agregar quando estivermos utilizando algum plugin em conjunto com o campo
      // plugins nesta versão só é disponibilizado com campos do tipo input
      'plugin': {
        // Indica qual o plugin sendo utilizado.
	// Obrigatório caso haja demanda de uso de plugins
        //   fastselect) Implementa o plugin fastselect - https://dbrekalo.github.io/fastselect/
	//   inputmask) Implementa o plugin inputmask - https://github.com/RobinHerbots/jquery.inputmask/
        'name':'fastselect',
        // É um objeto que indica as caracteristicas de configuração do plugin, cada um tem a sua característica
	// É obrigatório quando utilizando os plugins: fastselect
        'options': {
          'data-user-option-allowed': 'true',
          'data-url': '/ws/v1/getData',
          'data-load-once':'true',
          'data-initial-value': null,
          // value="new data,separator"
          // data-initial-value='[{"text": "new data", "value" : "new data"}, {"text": "separator", "value" : "separator"}]'
	},
	// É um array que indica os parâmetros que serão repassados ao plugin
	// Obrigatório para os plugins: inputmask
	// Para maiores exemplos veja o item "Plugins no wiki do github deste projeto"
	'params': [["(99) 9999-9999", "(99) 999.999.999"]]
      }
      // field icon. a estrutura do icon é ignorada em campos do tipo "select"
      'icon': {
        'image': 'fa-envelope',
        // field icon location (left or right, default left, deve conter apenas 'l' ou 'r' para representar a orientação)
        'orientation': null,
      },
      // botão de ação. a estrutura button é ignorada em campos do tipo "select"
      'button': {
        'image': null,
        'label': null,
        'orientation': null,
        // receaves a triggered function through the icon click action
        'trigger': null,
      },
      // whenever field is multiple options leave them here
      'options': [
        // selected is the default selection option
        // se value for vazio e o field for required o sistema irá gerar um erro de falta de preenchimento quando estiver sendo avaliado
        {'label': 'Selecione', 'value': '', 'default': true},
        {'label': 'Particular Email', 'value':'Particular'},
        {'label':'Comercial Email', 'value':'Comercial'}
      ],
      // contem uma função para renderizar a apresentação caso haja necessidade
      'render': null,
      // função para validação do field
      // a função a ser utilizada pode apresentar mensagens por meio da funcioalidade confirm ou alert, mas sempre deve retornar apenas verdadeiro ou falso.
      'validation': null,
      // texto que será apresentado logo abaixo do campo como um help inline do mesmo.
      'comment': null,
      // vazio se for um campo não obrigatório ou a mensagem a ser apresentada ao usuário caso seja um campo obrigatório
      'required': 'Você deve indicar o tipo do email!'
    }, {
      'label': 'Autorizo a divulgar este email', 'title': 'Publicado', 'type': 'ck',
      // presente apenas em campos do tipo checkbox e radio button, indica se os mesmos devem ser ou não selecionados.
      'default': false,
      'render': function (f) {return f.prop('checked')?'Sim':'Não';}
    },
    {'label': 'Descritivo', 'title': 'Descritivo', 'placeholder': 'Caso queira pode indicar o nome descritivo do email', 'type': 'i'},
    {'label': 'Observações', 'title': 'Observação', 'placeholder': 'Você pode deixar observações como email para avisos', 'type': 'i'},
    {'label': 'Email para Contato', 'title': 'Email', 'icon': {'image': 'fa-envelope'}, 'type': 'i', 'required': 'You must provide an email',
    }
  ]
};
```

## Licensing

One really important part: Give your project a proper license. Here you should
state what the license is and how to find the text version of the license.
Something like:

"The code in this project is licensed under [MIT license](https://github.com/rstriquer/BADE/blob/master/LICENSE)."
