{% if include.lowres == true %}
![{{ include.image-url }}](/assets/images/low{{ include.image-url }})
{% else %}
![{{ include.image-url }}](/assets/images{{ include.image-url }})
{% endif %}
[*See full picture by clicking here ↗*](/assets/images{{ include.image-url }}){:target="_blank"}
