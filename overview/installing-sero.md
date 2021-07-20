---
description: Can you make the leaderboard?
---

# Installing Sero Speedrun

## 3, 2, 1...

Ok, you need [Node LTS \(currently 14.x\) for your platform](https://nodejs.org/en/download/).

Next, install Sero.

{% tabs %}
{% tab title="Bash" %}
```bash
npm i @sero.run/sero
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
 Some shells may require using `npm i "@sero.run/sero"`
{% endhint %}

Start the default example server which includes the user guides content, with:

{% tabs %}
{% tab title="Bash" %}
```bash
npm run start
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Do you see `Server listening at http://0.0.0.0:8080` in your terminal? You can hit the timer on your speedrun because you're done!

You can validate the functionality of the example by navigating to the configuration URLs for either of the CDS Hooks or Rest modules.

[**http://localhost:8080/cds-services**](http://localhost:8080/cds-services)

[**https://localhost:8080/metadata**](https://localhost:8080/metadata)\*\*\*\*
{% endhint %}

