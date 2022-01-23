---
layout: default
title: Workshops and Events
---

<div class="">
  <div class="black lh-copy w-100 mt5">

    <h2 class="ttu pa5 bb b--near-white">Our Workshops and Events</h2>

    <div class="ph5 pv3 gray w-80">
      <p>
        We try to regularly organize events with our in-house baristas and
        dear guests from our community. Feel free to reach out to us if you are
        looking for a friendly place for this kind of events.
      </p>

      <p>
        Disclaimer: we might have to reach out to you and refund you if we're
        sold out due to our booking technical limitations. We're sorry and
        we still hope to see you soon!
      </p>
    </div>

    {% for event in site.data.events %}
      <div class="flex-l striped--near-white">
        <div class="w-70-l">

          {% if event.image_url %}
            <img src="{{event.image_url}}" alt="event.title" class="dn-l w-100" />
          {% endif %}

          <div class="pa5">
            <h3 class="mb0 tracked">{{ event.title }}</h3>

            <p class="tracked">
              <span class="underline">{{ event.date | date: "%A, %R on %-d of %B %Y" }}</span> by {{ event.author }}
            </p>

            <p>
              &#128176;
              {% if event.price != '0' %}
                €{{ event.price }}
              {% else %}
                free
              {% endif %}
              &nbsp;
              &#128099; Group of {{ event.slots }}
              &nbsp;
              &#8987; Takes {{ event.duration }}
            </p>

            <p class="measure-wide ">
            {{ event.description | newline_to_br }}
            </p>

            <p>
              {% assign unix_date = event.date | date: '%s' | times: 1 %}
              {% assign unix_cur_date = site.time | date: '%s' | times: 1 %}

              {% assign simple_date = event.date | date: '%c' %}
              {% assign payment_desc = event.title | append: ': ' | append: simple_date | url_encode %}
              {% if unix_date > unix_cur_date %}
                <a
                  href="https://www.vivapayments.com/web2/?ref=8156126989356884&requestAmount={{ event.price | times: 100 }}&lang=en-GB&color=EF3D28&notes={{ payment_desc }}"
                  class="bg-tym-red white pv3 ph4 dib link b tracked"
                >
                  Save my spot
                </a>
              {% else %}
                <span class="bg-gray white pv3 ph4 dib link b tracked pointer">
                  Sold out
                </span>
              {% endif %}
            </p>
          </div>
        </div>
        <div class="dn db-l w-30 contain" style="background-image: url('{{ event.image_url }}')">
        </div>
      </div>
    {% endfor %}
  </div>
</div>
