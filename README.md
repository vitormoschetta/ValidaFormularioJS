# ValidaFormularioJS

## Arquivo 'Validation.js':

```
validateState = false;

validateRequiredMsg = "Campo de preechimento obrigatorio";
validateMailMsg = "E-mail informado é invalido";
validateNumericMsg = "O valor deve ser numerico";
validateMinMsg = "A quantidade mínima de caracters é: ";
validateMaxMsg = "A quantidade máxima de caracteres é: ";
validatePasswordMsg = "Senhas não conferem";


function validate(form_id)
{
    $('#'+form_id+' :input').each(function(){
        /* required */
        if ( $(this).hasClass('required') && $.trim( $(this).val() ) == ""){
            $(this).addClass('invalid');
            $(this).focus();
			document.querySelector('#validate_message').innerText = validateRequiredMsg;
            validateState = false; 
            return false;
        }
        else{
            $(this).removeClass('invalid');
            validateState = true;
        }
		
         /* numeric value */
        if ( $(this).hasClass('required') && $(this).hasClass('numeric') ){
            var nan = new RegExp(/^[\d,.?!]+$/);
            if (!nan.test($.trim( $(this).val() ))){
                $(this).addClass('invalid');
                $(this).focus();
                document.querySelector('#validate_message').innerText = validateNumericMsg;
                validateState = false;
                return false;
            }
            else{
                $('#validate_message').html('');
                $(this).removeClass('invalid');                      
                validateState = true;
            }
        }
		
        /* mail */
        if ( $(this).hasClass('email') ){
            var er = new RegExp(/^[A-Za-z0-9_\-\.]+@[A-Za-z0-9_\-\.]{2,}\.[A-Za-z0-9]{2,}(\.[A-Za-z0-9])?/);
            if (!er.test($.trim( $(this).val() ))){
                 $(this).addClass('invalid');
                 $(this).focus();
				 document.querySelector('#validate_message').innerText = validateMailMsg;
                 validateState = false;
                 return false;
            }
            else{
                $(this).removeClass('invalid');
                validateState = true;
            }
        } 

        /* min value */
        if ( $(this).attr('min') && $(this).hasClass('required') ){
            if($.trim($(this).val()).length < $(this).attr('min') ){
                $(this).addClass('invalid');
                $(this).focus();
                document.querySelector('#validate_message').innerText = validateMinMsg + $(this).attr('min');
                validateState = false;
                return false;
            }
            else{
                $('#validate_message').html('');
                $(this).removeClass('invalid');
                validateState = true;
            }
        }
		
         /* max value */
        if ( $(this).attr('max')  && $(this).hasClass('required') ){
            if($.trim($(this).val()).length > $(this).attr('max') ){
                $(this).addClass('invalid');
                $(this).focus();
                document.querySelector('#validate_message').innerText = validateMaxMsg + $(this).attr('max');			
                validateState = false;
                return false;
            }
            else{
                $('#validate_message').html('');
                $(this).removeClass('invalid');
                validateState = true;
            }
        }		
        /* password */
        if ( $(this).hasClass('password') && $(this).nextAll('.password').hasClass('password')){ 
            if ($.trim( $(this).val() ) != $.trim( $(this).nextAll('.password').val() )){
                 $(this).nextAll('.password').addClass('invalid');
                 $(this).nextAll('.password').focus();
                 document.querySelector('#validate_message').innerText = validatePasswordMsg;
                 validateState = false;
                 return false;
            }
            else{ 
                $('#validate_message').html('');
                $(this).nextAll('.password').removeClass('invalid');
                validateState = true;
            }
        }           

    })
}
```


## Arquivo 'HTML':
```
<html>
  <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
  <link href="style.css" rel="stylesheet">

<body>
  <div class="content">

    <div id="mostrar" class="alert alert-danger" role="alert">    
        <label id="validate_message"></label>
    </div> 

    <form method="post" id="frm">
      
      <div class="form-group">
        <label for="exampleInputEmail1">Nome</label>
        <input type="text" name="nome" class="form-control required">
      </div>
      
      <div class="form-group">
        <label for="exampleInputEmail1">Altura</label>
        <input type="text" name="altura" class="form-control required numeric">          
      </div>      
      
      <input type="button" value="Gravar" class="btn btn-primary" onclick="Gravar()">
    </form>

  </div>


  <script  src="https://code.jquery.com/jquery-3.5.1.min.js"></script>
  <script  src="https://code.jquery.com/jquery-3.5.1.min.js"></script>
  <script src="validations.js"></script>
  <script>    
    var elMostrar = document.getElementById('mostrar');
    elMostrar.style.display = 'none';

    function Gravar() {
      validate('frm');            
      if (!validateState) {                          
          elMostrar.style.display = 'block';
          return;
      }    
      
      // Submeter formulário
      alert('Enviado');
    }
  </script>

  
</body>

</html>
```
