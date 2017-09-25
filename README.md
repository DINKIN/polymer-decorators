⚠ **Experimental!** This repository is a work in progress and may not work as expected. ⚠

[![Travis Build Status](https://travis-ci.org/Polymer/polymer-decorators.svg?branch=master)](https://travis-ci.org/Polymer/polymer-decorators)

# polymer-decorators

----

TypeScript decorators for Polymer 2.0

## Example

```typescript
import {customElement, property, query, queryAll, observe} from '../polymer-decorators/typescript/decorators.js';

// This sets the static `is` property and registers the element
@customElement('test-element')
class TestElement extends Polymer.Element {

  // @property replaces the static `property` getter.
  // The type is read from the type annotation, `notify` is the same as in
  // plain Polymer
  @property({notify: true})
  foo: number = 42;

  // @property replaces the static `property` getter.
  // The type is read from the type annotation, `reflectToAttribute` is the same as in
  // plain Polymer
  @property({reflectToAttribute: true})
  reflectFoo: string = 'opened';

  // @property replaces the static `property` getter.
  // The type is read from the type annotation, `readOnly` is the same as in
  // plain Polymer.  Read only properties must use a private generated
  // setter of the convention _setProperty(value). ex. _setReadOnlyBar(42)
  @property({readOnly: true})
  readOnlyBar: number;

  // This property doesn't fire bar-changed events
  @property()
  bar: string = 'yes';

  // @query replaces the property with a getter that querySelectors() in
  // the shadow root. Use this for type-safe access to internal nodes.
  @query('h1')
  header: HTMLHeadingElement;

  @queryAll('input')
  allInputs: HTMLInputElement[];

  // This method will be called when `foo` changes
  @observe('foo')
  private _fooChanged(newValue: number) {
    console.log(`foo is now: ${newValue}`);
  }

  // @observe can take an array of properties
  @observe(['foo', 'bar'])
  private _fooBarChanged(newFoo: number, newBar: string) {
    console.log(`foo is now: ${newFoo}, bar is now ${newBar}`);
  }

}
```