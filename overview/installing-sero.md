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

{% page-ref page="guides/cds-hooks/" %}

## Challenge mode

Want to get Sero started as a contributor? Clone the project:

```text
git clone https://github.com/Automate-Medical/sero.git
```

Remember, you need [Node LTS \(currently 14.17.x\) for your platform](https://nodejs.org/en/download/). Then, install the dependencies:

{% tabs %}
{% tab title="Bash" %}
```bash
npm install
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
That's... it actually. You should be able to build the project with `npm run build` and test it with `npm run test`
{% endhint %}

