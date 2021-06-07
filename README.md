# Shopify-variant-barcode
Make use of Shopifys variant barcode

1. Open snippets > product-form.liquid
2. Locate and replace this:

```  
<div class="product-add">
    {% if settings.show_quantity %}
      <div class="qty-selection">
        <h5><strong>{{ 'products.product.quantity' | t }}</strong></h5>
        <div class="quantity__wrapper">
          <a class="down quantity-control-down" field="quantity">-</a>
            <input min="1" type="text" name="quantity" class="quantity" value="1" />
          <a class="up quantity-control-up" field="quantity">+</a>
        </div>
      </div>
    {% endif %}

    <div class="note note-success mt3 js-added-msg" style="display: none">
    <b>{{ 'products.product.added' | t }}</b>&nbsp;&nbsp;&nbsp;<a class="underline" href="{{ routes.cart_url }}">{{ 'products.product.view_cart' | t }}</a> {{ 'products.product.or' | t }} <a class="underline" href="{{ routes.all_products_collection_url }}">{{ 'products.product.continue' | t }}</a>.
    </div>
    <div class="note note-error js-error-msg" style="display: none">
    <b>{{ 'cart.general.cart_error' | t }}</b>&nbsp;&nbsp;&nbsp;{{ 'cart.general.update_qty_error' | t }}
    </div>
    <input id="addToCart" type="submit" name="button" class="product__add-button add clearfix AddtoCart js-ajax-submit {% if settings.show_payment_button and product.selling_plan_groups.size == 0 %} secondary-button{% endif %}" value="{{ call_to_action }}" {% unless current_variant.available %}disabled{% endunless %} />

    {% if settings.show_payment_button %}
     {{ form | payment_button }}
    {% endif %}
  </div>
    <p class="product__add-msg add-to-cart-msg"></p>
```

With this:

```
{% if current_variant.barcode contains 'call' %}
<div class="call__us">Call us</div>
{% else %}
  <div class="product-add">
    {% if settings.show_quantity %}
      <div class="qty-selection">
        <h5><strong>{{ 'products.product.quantity' | t }}</strong></h5>
        <div class="quantity__wrapper">
          <a class="down quantity-control-down" field="quantity">-</a>
            <input min="1" type="text" name="quantity" class="quantity" value="1" />
          <a class="up quantity-control-up" field="quantity">+</a>
        </div>
      </div>
    {% endif %}

    <div class="note note-success mt3 js-added-msg" style="display: none">
    <b>{{ 'products.product.added' | t }}</b>&nbsp;&nbsp;&nbsp;<a class="underline" href="{{ routes.cart_url }}">{{ 'products.product.view_cart' | t }}</a> {{ 'products.product.or' | t }} <a class="underline" href="{{ routes.all_products_collection_url }}">{{ 'products.product.continue' | t }}</a>.
    </div>
    <div class="note note-error js-error-msg" style="display: none">
    <b>{{ 'cart.general.cart_error' | t }}</b>&nbsp;&nbsp;&nbsp;{{ 'cart.general.update_qty_error' | t }}
    </div>
    <input id="addToCart" type="submit" name="button" class="product__add-button add clearfix AddtoCart js-ajax-submit {% if settings.show_payment_button and product.selling_plan_groups.size == 0 %} secondary-button{% endif %}" value="{{ call_to_action }}" {% unless current_variant.available %}disabled{% endunless %} />

    {% if settings.show_payment_button %}
     {{ form | payment_button }}
    {% endif %}
  </div>
    <p class="product__add-msg add-to-cart-msg"></p>
{% endif %}
```

3. When done open the product within Shopifys main admin and scroll down to the Variants section
4. Add **call** into the barcode field for each variant where you would prefer "Call us" inplace of the Add to Cart button + Save
