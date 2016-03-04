# ir-recursive

**A templated recursive element for Polymer 1.0**

## What it does
Represent object tree while leaving you in total control of the actual presentation. 
Provides only the recursion and basic collapse/expand functionality (for now).

### This is now at a totally experimental stage.

## Sample usage

		<ir-recursive max-depth="1">
			<template class='item'>  
				<style>
					.wrapper { display: inline-block; box-shadow : 0px 0px 10px lightblue; margin-top : 10px; }
					[children-toolbar] { background : lightblue; padding : 3px 0 3px 5px }
					.content { display : block; padding : 10px 0 10px 10px; } 
					.lm { padding-left : 10px; margin-bottom : 10px; }
					paper-icon-button { width : 20px; font-size : 10px; } 
					.xxxcontent { padding : 10px }
				</style>
				<div class="wrapper">
					<div class="xxxcontent">
						<input type="checkBox" value="[[ data.content ]]">
						<b>{{ data.title }}</b>
						<input value="[[ data.content ]]">
						<div children-toolbar>
							<paper-icon-button icon="expand-more" expand></paper-icon-button>
							<paper-icon-button icon="expand-less" collapse></paper-icon-button>
						</div>
					</div>
					<div class="lm children"></div>
				</div>
			</template>
		</ir-recursive>

## Contribution
Issues and pull requests are most welcome. Fork it [here](https://github.com/IgorRubinovich/ir-textarea).

## License
[MIT](http://opensource.org/licenses/MIT) 

