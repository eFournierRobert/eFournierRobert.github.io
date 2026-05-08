{% if include.online %}
![{{ include.image-url }}]({{ include.image-url }})
{% else %}
{% if include.lowres == true %}
![{{ include.image-url }}](/assets/images/low{{ include.image-url }})
{% else %}
![{{ include.image-url }}](/assets/images{{ include.image-url }})
{% endif %}
{% endif %}
{% if include.online != true %}
[*See full picture by clicking here ↗*](/assets/images{{ include.image-url }}){:target="_blank"}
{% else %}
[*See original picture by clicking here ↗*]({{ include.image-url }}){:target="_blank"}
{% endif %}
