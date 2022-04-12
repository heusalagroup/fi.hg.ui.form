# @heusalagroup/fi.hg.ui.components

Core UI library for our commercial Form App software.

For now this repository is mostly for [issue tracking](https://github.com/heusalagroup/fi.hg.ui/issues) and demo purposes.

### It doesn't have many runtime dependencies (if any)

This library expects some of our libraries to exist in relative paths:

 * [@heusalagroup/fi.hg.core](https://github.com/heusalagroup/fi.hg.core) to be located in the relative path `../../ts`
 * [@heusalagroup/fi.hg.ui.services](https://github.com/heusalagroup/fi.hg.ui.services) to be located in the relative path `../services`
 * [@heusalagroup/fi.hg.ui.components](https://github.com/heusalagroup/fi.hg.ui.components) to be located in the relative path `../components`

The only 3rd party dependency we have is for [Lodash library](https://lodash.com/).

### We don't have traditional releases

This project evolves directly to our git repository in an agile manner.

This git repository contains only the source code for compile time use case. It is meant to be used as a git submodule 
in a NodeJS or webpack project.

Recommended way to initialize your project is like this:

```
mkdir -p src/hg/ui

git submodule add git@github.com:heusalagroup/fi.hg.core.git src/hg/ts
git config -f .gitmodules submodule.src/hg/ts.branch main

git submodule add git@github.com:heusalagroup/fi.hg.ui.services.git src/hg/ui/services
git config -f .gitmodules submodule.src/hg/ui-services.branch main

git submodule add git@github.com:heusalagroup/fi.hg.ui.components.git src/hg/ui/components
git config -f .gitmodules submodule.src/hg/ui-components.branch main

git submodule add git@github.com:heusalagroup/fi.hg.ui.form.git src/hg/ui/form
git config -f .gitmodules submodule.src/hg/ui-form.branch main
```

Only required dependency is to [the Lodash library](https://lodash.com/):

```
npm install --save-dev lodash @types/lodash
```

Some of our code may use reflect metadata. It's optional otherwise.

```
npm install --save-dev reflect-metadata
```

### Commercial support

For commercial support check [Sendanor's organization page](https://github.com/sendanor).

## Demo app

UI form builder demo available at [lomake.app](https://www.lomake.app/builder).

### The iframe demo

Here's an iframe POC how to use the form model on outside website:

```html
<div id="iframe-container"></div>

<script src="https://www.lomake.app/libs/nor-ui-frame.min.js"></script>

<script>
(function() {

    const iframe = window.nor.uiFrame.init('iframe-container');

    iframe.on("submit", (data) => {
        console.log('SUBMIT: ', data)
    });

    iframe.on("cancel", () => {
        console.log('CANCEL')
    });

    iframe.setModel({
        "title": "Test form",
        "items": [
            {
                "type": "text-field",
                "key": "customer.firstName",
                "label": "First name"
            },
            {
                "type": "text-field",
                "label": "Last name",
                "key": "customer.lastName"
            },
            {
                "type": "text-field",
                "label": "Email",
                "key": "customer.email"
            },
            {
                "type": "text-area-field",
                "key": "order.summary",
                "placeholder": "Summary of order"
            }
        ]
    });

})();
</script>

```

Although it may already partially work, ***this is just a POC***. We may change the API at any moment!

The model for `iframe.setModel()` can be created using [lomake.app/builder](https://www.lomake.app/builder).

This example is also available at [./examples/test-iframe.html](https://github.com/heusalagroup/fi.hg.ui/blob/main/examples/test-iframe.html) as well as online at [lomake.app/test-iframe.html](https://www.lomake.app/test-iframe.html).

### React component

We also have a react component to render the form -- but it has not been released yet. Our builder's preview uses it.

```jsx
<Form
    model={formModel}
    value={valueModel}
    change={(value) => {}}
    submit={() => {}}
    cancel={() => {}}
/>
```

### License

Copyright (c) Heusala Group. All rights reserved. Licensed under the MIT License (the "[License](./LICENSE)");
