---
layout: wrapper
page_type: /assets/css/recipe-page.css
---

<!-- 
  Adding recipe metadata docs: 
    - https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/itemscope#html 
    - https://schema.org/Recipe
-->

<div itemscope itemtype="https://schema.org/Recipe">

  <img itemprop="image" src="{{ page.image }}"/>
  <h1 itemprop="name">{{ page.title }}</h1>
  <time datetime="{{ page.date }}">{{ page.date }}</time>
  <div itemprop="description">{{ page.excerpt }}</div>
  
  {{content}}

  <!-- metadata --> 
  {% if page.prepTime or page.cookTime or page.yield %}
    <ul>
      {% if page.yield %}<li>Yield: <span itemprop="recipeYield">{{ page.yield.value }} {{ page.yield.unit }}</span></li>{% endif %}
      {% if page.prepTime %}<li>Preparation time: {% include duration.html itemProp="prepTime" hour=page.prepTime.hour min=page.prepTime.min %}</li>{% endif %}
      {% if page.cookTime %}<li>Cooking time: {% include duration.html itemProp="cookTime"  hour=page.cookTime.hour min=page.cookTime.min %}</li>{% endif %}
      {% if page.totalTime %}<li>Total time: {% include duration.html   hour=page.totalTime.hour min=page.totalTime.min %}</li>{% endif %}
    </ul>
  {% endif %}

  <!-- ingredients -->
  <div>
    <h3>Ingredients</h3>
     <ul>
        {%- for ingredient in page.ingredients -%}
        <li itemprop="recipeIngredient" itemscope itemtype="https://schema.org/PropertyValue"><span itemprop="value">{{ ingredient["value"] }}</span>{% if ingredient["unit"] %} {{ ingredient["unit"] }}{% endif %} <span itemprop="name">{{ ingredient["name"] }}</span>{% if ingredient["optional"] %} (optional){% endif %}</li>
        {%- endfor -%}
     </ul>
  </div>

  <!-- instructions -->
  <div itemprop="recipeInstructions">
    <h3>Instructions</h3>
    {%- for instruction in page.instructions -%}
    {% if instruction.title %}<h4>{{ instruction.title }}</h4>{% endif %}
    <ol>
      <li>{{ instruction.steps | join: '</li><li>' }}</li>
    </ol>
    {%- endfor %}
  </div>

  <!-- faq -->
  <div>
    <h3>FAQ</h3>
    {%- for item in page.faq -%}
    <details>
      <summary>{{ item.question }}</summary>
      {{ item.answer }}
    </details>
    {%- endfor %}
  </div>

</div>