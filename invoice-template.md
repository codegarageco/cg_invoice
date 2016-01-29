
# {{page.title}} <a class="pdf-link" href="{{page.pdf_url}}" target="_blank"><span class="mega-octicon octicon-file-pdf"></span></a>

## Invoice description

This invoice is for work performed by _{{site.person_name}}_ for _{{site.client}}_.


__Invoice Number:__ {{ page.invoice_number }} \\
__Date:__ {{ page.date | date_to_string }} \\
__For period:__ {{ page.period }}

## Invoice line items

{% assign total = 0 %}
{% assign hours = 0 %}
|__Description__|__Hourly rate__|__Hours__|__Total__|
|---|---:|---:|---:|{% for item in page.invoice_line_items %}{% assign amount = page.hourly_rate | times:item.hours %}{% assign total = total | plus:amount %}{% assign total_hours = total_hours | plus:item.hours %}
|{{item.title}}|{{page.hourly_rate}} {{page.invoice_currency}}|{{item.hours}}|{{amount}} {{page.invoice_currency}}|{% endfor %}
|||{{total_hours}}|__{{total}} {{page.invoice_currency}}__|

## Bank Information

{{page.invoice_payment_info}}
