# shopify-cart-custom-fields
Code snippets to capture more information in Shopify cart page:
1. Delivery date selection using [flatpickr](https://flatpickr.js.org) date picker control
2. Delivery time slot selection
3. Text area input

## Steps
1. In **layout/theme.liquid**, `<head>` section, add the [flatpickr](https://flatpickr.js.org) css and js refrence
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/flatpickr/dist/flatpickr.min.css">

<script src="https://cdn.jsdelivr.net/npm/flatpickr" defer="defer"></script>
```
2. In **sections/cart-template.liquid**, add the delivery date selection
```html
<label for="flatpickr" class="label--hidden">Delivery/Collection Date</label>

<input name="attributes[Delivery or Collection Date]" id="flatpickr" class="input-full" placeholder="Choose delivery/collection date" value="{{ cart.attributes.date }}">
```
3. In **sections/cart-template.liquid**, add the delivery time slot selection
```html
<label for="CartTime">Timeslot</label>

<select class="single-option-selector" data-option="option1" id="CartTime" name="attributes[Timeslot]">

<option value="9 AM - 1 PM"{% if cart.attributes["Timeslot"] == "9 AM - 1 PM" %} selected{% endif %}>9 AM - 1 PM</option>

<option value="2 PM - 6 PM"{% if cart.attributes["Timeslot"] == "2 PM - 6 PM" %} selected{% endif %}>2 PM - 6 PM</option>

<option value="6 PM - 10 PM"{% if cart.attributes["Timeslot"] == "6 PM - 10 PM" %} selected{% endif %}>6 PM - 10 PM</option>

</select>
``` 
4. In **sections/cart-template.liquid**, add the delivery time slot selection
```html
<label for="CartMessage" class="label--hidden">Write a message for your recepient</label>

<textarea name="attributes[Card Message]" id="CartMessage" class="input-full" placeholder="Write a message for your recepient (max 150 characters)">{{ cart.attributes["Message"] }}</textarea>
```
5. In **assets/theme.js.liquid**, initialise the [flatpickr](https://flatpickr.js.org) date control and set its [options](https://flatpickr.js.org/options/)
```javascript
$('#flatpickr').flatpickr({
    dateFormat: "D, d M Y",
    minDate: new Date().fp_incr(2),
    disableMobile: "true",
    disable: ["Sat, 11 Jan 2020","Sat, 18 Jan 2020",
              {
            from: "Sat, 25 Jan 2020",
            to: "Sun, 2 Feb 2020"
        }
    ]
  });
```

## References
* [flatpickr](https://flatpickr.js.org) date picker control options https://flatpickr.js.org/options/
* Shopify cart attribute generator https://ui-elements-generator.myshopify.com/pages/cart-attribute
* Shopify cart attribute doc https://shopify.dev/docs/liquid/reference/objects/cart