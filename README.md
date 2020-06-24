- with email-preview as dependency (transitive from email-templates)

```
npm install email-templates pug --save

rm -rf node_modules
npm install
du -sh node_modules
 50M    node_modules

rm -rf node_modules
npm install --production
du -sh node_modules
 50M    node_modules
```

Whether we use the production flag or not, email-preview is fetched inside node_modules.

- with email-preview as a dev dependency and no more transitive dependency through email-templates

```
npm install git://github.com/astik/email-templates.git#without-preview-email pug --save

rm -rf node_modules
npm install
du -sh node_modules
 30M    node_modules
```

Node modules is 20Mo lighter without email-preview.

```
npm install preview-email --save-dev

rm -rf node_modules
npm install
du -sh node_modules
 50M    node_modules

rm -rf node_modules
npm install --production
du -sh node_modules
 30M    node_modules
```

In dev (without production flag), we have the email-preview dependency and a 50Mo node_modules: this is expected.
In production (with production flag), bundle is back to 30Mo as email-preview is not fetched anymore.

Having a lighter production node_module folder is better:

- for those running container, this means a much lighter container
- it reduces deployed flag, which reduces potential vulnerabilities
