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
  {% if page.prepmins or page.cookmins %}
    <ul>
      {% if page.yield %}<li>Yield: <span itemprop="recipeYield">{{ page.yield.value }} {{ page.yield.unit }}</span></li>{% endif %}
      {% if page.prepmins %}<li>Preparation time: <time datetime="PT{{ page.prepmins }}M" itemprop="prepTime">{{ page.prepmins }} mins</time></li>{% endif %}
      {% if page.cookmins %}<li>Cooking time: <time datetime="PT{{ page.cookmins }}M" itemprop="cookMins">{{ page.cookmins }} min</time></li>{% endif %}
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

</div>