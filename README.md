#Configuration Plugin

The Configuration plugin is an extremely useful way to store site-wide configuration.  The configuration plugin stores
your configuration into your database and is made available throughout your site (views, controllers, models, tasks, etc...)

##About
CakePhp 2.x
Version: 1.1
Author: Nick Baker
Email: nick@webtechnick.com
Website: http://www.webtechnick.com
Updates: http://www.webtechnick.com/blogs/view/223/CakePHP_Configuration_Plugin


##Install

1) Copy the plugin files into /app/Plugin/Configuration
2) run

		cake schema create --plugin Configuration


========================= Setup =========================
1) Open up your app_controller.php file and add:

		public $uses = array('Configuration.Configuration');
	
		public function beforeFilter(){
			//Load Configurations
			$this->Configuration->load($prefix); //$prefix is 'CFG' by default
		}
  
2) Navigate to http://www.yoursite.com/admin/configuration/configurations
3) Start adding configurations.


========================= Usage =========================
Whatever name/value pair you save in your configuration database, you'll have access to anywhere in your site via
  
	Configure::read('[prefix].[name]'); //returns 'value';
  
  
========================= Example =========================
Say I have a configuration table like so:
  
__ID__|_NAME______|_VALUE_________________
  1   | email     | nick@webtechnick.com
  2   | name      | Nick Baker
  
  
I could access this data anywhere in my app by simply using `Configure::read([prefix].[name]);`
(Default prefix is 'CFG', but you can change it in your AppController.php).

In a view:
	$this->Html->link('Email ' . Configure::read('CFG.name'), 'mailto:' . Configure::read('CFG.email'));

In a controller:
	$this->Email->from = Configure::read('CFG.email');

In a model: 
	$this->findByEmail(Configure::read('CFG.email'));


You can get your entire Configuration table by not giving a name: 
`Configure::read('CFG');` //return an associative array of your configuraitons database.
