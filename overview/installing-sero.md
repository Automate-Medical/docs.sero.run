---
description: Can you make the leaderboard?
---

# Installing Sero Speedrun

## 3, 2, 1...

Ok, you need [Node LTS \(currently 14.17.x\) for your platform](https://nodejs.org/en/download/).

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

{% hint style="success" %}
Did the install complete? You're done! Wow, that was fast. Try the challenge mode below or continue on to our first User Guide.
{% endhint %}

{% page-ref page="user-guides/start-a-cds-hooks-api.md" %}

## Challenge mode

Want to get Sero started as a contributor? Clone the project:

```text
git clone https://github.com/Automate-Medical/sero.git
```

Install the dependencies \(use `npm ci` for the speed boost\) and start the default example server which includes the user guides content, with:

{% tabs %}
{% tab title="Bash" %}
```bash
npm ci
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

