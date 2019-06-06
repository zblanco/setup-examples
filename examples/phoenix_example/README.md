# Using Tailwind CSS with the Phoenix Framework

Assuming you've already [installed Elixir/Erlang and Phoenix](https://hexdocs.pm/phoenix/installation.html) and ran the `mix phx.new` command to generate a app we can now:

  * Install dependencies with `mix deps.get`
  * Create and migrate the database with `mix ecto.setup`
  * Install Node.js dependencies with `cd assets && npm install`

Then while we're in `/assets` we can install Tailwind:

```sh
npm install tailwindcss --save-dev
```

Followed by PostCSS:

```sh
npm install postcss-loader --save-dev
```

Now we can create a `postcss.config.js` file (again in the same `/assets` directory).

```js
module.exports = {
    plugins: [
        require('tailwindcss'), 
        require('autoprefixer')
    ],
}
```

And configure `webpack.config.js` to use PostCSS.
```js
{
  test: /\.css$/,
  use: [
    MiniCssExtractPlugin.loader, 
    'css-loader',
    'postcss-loader', 
  ]
}
```

Finally we'll bring in the Tailwind styles into the contents of our `/assets/css/app.css` file with:

```css
@tailwind base;
@import "./phoenix.css"; /* remove default css if desired */
@tailwind components;
@tailwind utilities;
```

Now outside of our `/assets` folder we can run our server with

```sh
mix phx.server
```

And visit [`localhost:4000`](http://localhost:4000) from our browser.

---

Check out the [Phoenix Docs](https://hexdocs.pm/phoenix/overview.html#content) for more detailed guides and tutorials about the framework.
