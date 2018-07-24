
# {{page.title}} <a class="pdf-link" href="{{page.pdf_url}}" target="_blank"><span class="mega-octicon octicon-file-pdf"></span></a>

## Description

This invoice is for work performed by _{{page.person_name}}_ for _{{page.client}}_.


__Invoice Number:__ {{ page.invoice_number }} \\
__Date:__ {{ page.date | date_to_string }} \\
__For period:__ {{ page.period }}

## Line items

{% assign total = 0 %}
{% assign hours = 0 %}
|__Description__|__Hourly rate__|__Hours__|__Total__|
|---|---:|---:|---:|{% for item in page.invoice_line_items %}{% if item.hourly_rate %}{% assign hourly_rate = item.hourly_rate %}{% else %}{% assign hourly_rate = page.hourly_rate %}{% endif %}{% assign amount = hourly_rate | times:item.hours %}{% assign total = total | plus:amount %}{% assign total_hours = total_hours | plus:item.hours %}
|{{item.title}}|{{hourly_rate}} {{page.invoice_currency}}|{{item.hours}}|{{amount}} {{page.invoice_currency}}|{% endfor %}
|||{{total_hours}}|__{{total}} {{page.invoice_currency}}__|
{% if page.exchange_rate > 0 %}
Exchange Rate {{page.exchange_rate}}, total payable in {{page.exchange_currency}}, **{{total | times:page.exchange_rate | round}} {{page.exchange_currency}}**
{% endif %}


## Bank Information

{{page.invoice_payment_info}}

{{page.address}}

{{page.note}}
