# custom-registry

With the advent of the [scoped custom element registry](https://github.com/whatwg/html/issues/10854), it seems that the platform has no appetite in creating new registries for purposes other than custom elements.  Based on this, this project is exploring ways that alternative registries for things like custom element enhancements could leverage the infrastructure of custom element registries, and peg their hopes on what the platform provides.

```TypeScript
export const enhancementRegistryKey = Symbol.for('M-3jKkLzvESqU_bRwgv0-w');
class YourElement extends HTMLElement {
    constructor() {
        super();
        const shadow = this.attachShadow({mode: 'open'});
        const div = document.createElement('div');
        div.textContent = 'Hello from Inner Shadow DOM';
        shadow.appendChild(div);
    }
}
const registry = new CustomElementRegistry();
const customEnhancementRegistry = new CustomEnhancementRegistry();
registry[enhancementRegistryKey] = customEnhancementRegistry;
registry.define('your-element', YourElement, {});
```

