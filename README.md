##Chrome Cookies

Dump **Google Chrome** `cookies` for a `url` to `stdout`.

### Installation

```bash
npm install -g chrome-cookies
```

[![NPM](https://nodei.co/npm/chrome-cookies.png)](https://nodei.co/npm/chrome-cookies/)

### Examples

```bash
chrome-cookies https://www.google.com/
```

This will output your google chrome browser cookies for `https://www.google.com/` into `stdout`.


```bash
chrome-cookies https://www.example.com/ > cookies.txt
```

This will output your google chrome browser cookies for `https://www.example.com/` into a new file called `cookies.txt`, in the current directory.

You can easily use this `cookies.txt` with `curl` like -

```bash
curl -b cookies.txt https://www.example.com/
```

or, with `wget` like -

```bash
wget --load-cookies cookies.txt https://google.com/
```

---
Thanks for using :)
