# ir-recursive

**A templated recursive element for Polymer 1.0**

## What it does
Represent object tree while leaving you in total control of the actual presentation. 
Provides only the recursion and basic collapse/expand functionality (for now).

### This is now at a totally experimental stage.

## Sample usage

		<ir-recursive id="testRec" max-depth="1">
			<template script-t>
				<script>
					document.querySelector('#testRec').addEventListener('script-ready', function() { 
						this.transformData = function() { 
							var tree = { 
									id : 0,
									title : "Категории",
									content : "",
									children : []
								};

								var categoryList = {};

								this.reqData.forEach(function(el) {
									if(el['postcategory']) 
									{
										var elId = el.postcategory[0].id,
											elTitle = el.postcategory[0].title,
											elContent = el.postcategory[0].content;

										if(!categoryList[elTitle])
										{
											categoryList[elTitle] = elTitle;
											var cObj = {
													id : elId,
													title : elTitle,
													content : elContent,
													children : [ {
															id : el.id,
															title : el.title,
															content : el.content
														} ]
												};
											tree.children.push(cObj);
										} 
										else 
											for(var i = 0; i < tree.children.length; i++) 
												if(tree.children[i].title == elTitle) 
													tree.children[i].children.push({ id : el.id, title : el.title, content : el.content });
									} 
									else 
										if(!categoryList[el.title]) 
											tree.children.push({ id : el.id, title : el.title, content : el.content, children : [] });
								}.bind(this));

								this.tree = tree;
								console.log(this.tree);
						}; 
					})
					</script>
				</template>
				<template item>
					<style>
						.wrapper { display: inline-block; box-shadow : 0px 0px 10px lightblue; margin-top : 10px; }
						[children-toolbar] { background : lightblue; padding : 3px 0 3px 5px }
						.content { display : block; padding : 10px 0 10px 10px; }
						.lm { padding-left : 10px; margin-bottom : 10px; }
						paper-icon-button { width : 20px; font-size : 10px; }
						.xxxcontent { padding : 10px }
					</style>
					<div class="wrapper">
						<div class="xxxcontent" content>
							<input type="checkBox" value="[[ data.content ]]">
							<b>{{ data.title }}</b>
							<input value="[[ data.content ]]">
							<div children-toolbar>
								<div nav-group>
									<paper-icon-button icon="expand-more" expand></paper-icon-button>
									<paper-icon-button icon="expand-less" collapse></paper-icon-button>
								</div>
								<paper-icon-button icon="create" edit-button></paper-icon-button>
								<paper-icon-button icon="add-box" create-button></paper-icon-button>
								<paper-icon-button icon="delete" delete-button></paper-icon-button>
							</div>
						</div>
						<div class="lm children"></div>
					</div>
				</template>
				<template edit>
					<p>Edit</p>
					<div edit-nav>
						<paper-icon-button icon="close" close-button></paper-icon-button>
					</div>
				</template>
				<template create>
					<p>Create</p>
					<div create-nav>
						<paper-icon-button icon="close" close-button></paper-icon-button>
					</div>
				</template>
				<template delete>
					<p>Delete</p>
					<div delete-nav>
						<paper-icon-button icon="close" close-button></paper-icon-button>
						<paper-button simple-delete>Delete</paper-button>
						<paper-button delete-with-child-nodes>Delete with child Nodes</paper-button>
						<paper-button recursive-delete>Recursive delete</paper-button>
					</div>
				</template>
		</ir-recursive>

## Contribution
Issues and pull requests are most welcome. Fork it [here](https://github.com/IgorRubinovich/ir-textarea).

## License
[MIT](http://opensource.org/licenses/MIT) 

