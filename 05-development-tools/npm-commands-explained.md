# `npm start` vs `npm run start`

### Interactive Demo

**Here are two equivalent commands:**

```bash
# Option 1 (Shortcut)
npm start

# Option 2 (Full command)
npm run start
```

**Both commands above do exactly the same thing!**

**Try it yourself:**
---
* Copy either command
* Both will execute the `"start"` script from your `package.json`
* The first one is just a convenient shortcut

Now I don't know exactly when I found this, but I was creating a project and I found out that `npm start` and `npm run start` are basically the same thing.

And I was like damn! I didn't know that.

Immediately one question came to mind:

> **Why don't we write `run` when using `start`? Is this thing only reserved for the `start` keyword or for some other keywords too?**

## What I Learned

* `npm start` is a shortcut for `npm run start`.
* The same applies to a few other built-in scripts: `npm test`, `npm stop`, and `npm restart`.
* For all other custom scripts, you **must** use `npm run <script-name>`.

This behavior is part of how npm handles built-in lifecycle scripts.

### 📋 Built-in Script Shortcuts

---

#### Scripts that work WITHOUT `run`:

* ✅ `npm start` = `npm run start`
* ✅ `npm test` = `npm run test`
* ✅ `npm stop` = `npm run stop`
* ✅ `npm restart` = `npm run restart`

#### Scripts that REQUIRE `run`:

* ❌ `npm dev` → **will not work**
* ✅ `npm run dev` → **required**
* ❌ `npm build` → **will not work**
* ✅ `npm run build` → **required**

### Example:

---

```json
"scripts": {
  "start": "node app.js",
  "dev": "vite"
}
```

**Commands:**

* `npm start` or `npm run start` → both will work
* `npm dev` → will **not** work
* `npm run dev` → required

### 🤔 Why does this happen?

---

#### The Technical Reason

npm has a set of predefined "lifecycle scripts" that get special treatment. These are:

* `start`, `stop`, `restart`, `test`

For these scripts, npm automatically creates shortcuts so you don't need to type `run`.

For any custom scripts you create (like `dev`, `build`, `deploy`, etc.), you must use the full `npm run <script-name>` syntax.

This is hardcoded into npm's behavior and is part of the official npm specification.

## Reference

I found this helpful Stack Overflow discussion while researching the topic:
[Is there a difference between `npm start` and `npm run start`?](https://stackoverflow.com/questions/51358235/is-there-a-difference-between-npm-start-and-npm-run-start)