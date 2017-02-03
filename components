# Ember Notes

## Components:
 Components are isolated from their surroundings, any data Components need has to be passed in.

 #### example:

app/templates/Components/Product-card.hbs


          <div class="Product-card">
          <h1>{{name}}</h1>
          <p>{{barcode}}</p>
          etc.
          </div>

app/routes/Product-card-doc.js


          export default Ember.Route.extend({
          model() {
          return this.store.findAll('product');
          }
          });

  In order to make a  property available to a component you must pass it in(e.g {{name}}, {{barcode}}) product-card is the component: we pass name, and barcode properties.

          e.g in index.
          {{#each model as |product|}}
          {{product-card name=post.name barcode=post.barcode}}
          {{/each}}


## Positional Params
 you can also pass parameters by position.
 for example:

         {{#each model as |product|}}
         {{product-card post.name post.barcode}
         {{/each}}
  To set up components to receive positional parameters you MUST set the
  positionalParams
  in attribute in your component class.

  app/components/product-card.js

          const ProductCardComponent = Ember.Component.extend({});

          ProductCardComponent.reopenClass({
          positionalParams: ['title',  'body']
          });

         export default ProductCardComponentl;

    This allows those attributes/properties in the component exactly as if they had been passed in eg.

        {{product-card name=post.name barcode=post.barcode}  

   Positional params are always declared on the component class and cannot be changed while an application runs.        

   more on positional params at Ember.js. Have not used thus far.

## Wrapping Content in a Component   

  Sometimes you want to define a component that wraps content provided by other templates.
  For example we will use product-card component that we can use in our application.

  app/templates/components/product-card.hbs

      <h1>{{name}}</h1>
      <div class="barcode">{{barcode}}</div>

  We can now pass product-card components properties to another template.
  eg.
      {{product-card name=name barcode=barcode}}

These examples the content we displayed comes from our model.
  -What if we want our component to be able to provide custom HTML content?

Components also support being used in BLOCK FORM.
  - example of a component block:
  - Block form always use # beginning of component name.
  - {{yield}} tells Ember that this content will be provided when the component is used.
    - components can be passed a Handlebars template that is rendered inside the component's template wherever the {{yield}} expression appears.

  app/templates/components/product-card.hbs

        <h1>{{name}}</h1>
        <div class="barcode">{{yield}}</div>


  - (index.hbs in most examples, but for vendnovation i use product-card-doc as index)
  - example of a component block:
  app/template/(INDEX)product-card-doc.hbs

        {{#product-card name=name}}
        <p class="author">by {{author}}</p>
        {{barcode}}
        {{/product-card}}



## Sharing Component Data with its Wrapped Content

-There is aslo a way to share data whitin you product-card component with the content it is wrapping.
-an example is in product-card component we will provide a way for user to configure what type of style they want to write in their post.

          app/template/product-card-doc(index).hbs

          {{#product-card editStyle="markdown"}}
          <p class="name">by {{name}}</p>
          {{body}}
          {{/product-card}}

- Supporting different editing styles requires different body components base on editing style. You can {{yield}} the component using the component HELPER and HASH helper.

        app/templates/components/product-card.hbs

        <h2>{{name}}</h2>
        <div class="body">{{yield (hash body=(component editStyle))}}</div>
