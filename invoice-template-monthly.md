
# {{page.title}} <a class="pdf-link" href="{{page.pdf_url}}" target="_blank"><span class="mega-octicon octicon-file-pdf"></span></a>

## Description

This invoice is for work performed by _{{page.person_name}}_ for _{{page.client}}_.


__Invoice Number:__ {{ page.invoice_number }} \\
__Date:__ {{ page.date | date_to_string }} \\
__For period:__ {{ page.period }}

{{page.note}}

## Line items

{% assign total = 0 %}
|__Description__|__Total__|
|---|---:|{% for item in page.invoice_line_items %}{% assign total = total | plus:item.amount %}
|{{item.title}}|{{item.amount}}|{% endfor %}
||__{{total}} {{page.invoice_currency}}__|

{% if page.exchange_rate > 0 %}
Exchange Rate {{page.exchange_rate}}, total payable in {{page.exchange_currency}}, **{{total | times:page.exchange_rate | round}} {{page.exchange_currency}}**
{% endif %}

## Bank Information

{{page.invoice_payment_info}}

