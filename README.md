# Install
composer require doc-space/nusoap

# Run a SoapServe

```
<?php
require('vendor/autoload.php');

ini_set("display_error", 'on');
ini_set("soap.wsdl_cache_enabled", "0");
$server = new Nusoap\soapServer();

$server->configureWSDL('foo', "urn:foo");
$server->wsdl->schemaTargetNamespace = "urn:foo";

$server->register(	
                    'classname.funcname', 
                    array( 
                                    'par_1' => 'xsd:integer', 
                                    'par_2'   => 'xsd:string', 
                    ), 
                    array('return' => 'xsd:Array'), 
                    "urn:foo", 
                    "urn:foo#funcname", 'rpc', 'encoded', 'Description foo bar'
                    );


class classname {
    public function funcname($par_1,$par_2) {
        return ['par_1' => $par_1, 'par_2' => $par_2, 'itens' => ['foo','bar']];
    }
}

$server->service(file_get_contents("php://input"));
?>
```
