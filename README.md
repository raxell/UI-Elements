# UI Elements

Some good readings on CSS organization that inspired the following conventions:

* https://github.com/trello/trellisheets/blob/master/styleguide.md
* https://github.com/mobify/mobify-code-style/tree/master/css/class-naming-conventions
* https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/


## Documentation

The documentation of a component must be placed directly in the file where it is
declared, in the form of docblock-like comments.
The documentation must include all you need to know about the component: purpose, special
behaviors, example code, etc.. Only by looking the CSS file you must figure out how to use
a particular component.
The docblock-like comments should be as follow:

    /**
     * Component name
     * ==============
     *
     * Description of the component and its behaviors.
     *
     * Example code:
     * ```
     *   <div class="component"></div>
     * ```
     *
     * Notes:
     * 1) explain why you put this property
     */
    .component {
        ...
        width: 100%; /* 1 */
        ...
    }

        /**
         * Sub-component name
         * ------------------
         *
         * Description of the sub-component and its behaviors.
         *
         * Example code:
         * ```
         *   ...
         * ```
         *
         * Notes:
         * 1) ...
         */
        .sub-component {
            ...
        }

            .sub-component-child {
                ...
            }

The text in the comment use a subset of markdown.
The *Notes* block is used to explain the usage of a particular CSS property that could
be misunderstood. Don't abuse it.


## Conventions

* One file per component

* Class names are kebab-case (*words-are-dash-separated*)

* CSS properties are ordered alphabetically

* Utility classes starts with `u-`, state classes start with `is-` and modifier classes
starts with `mod-`

* Define state classes after modifiers in source-order to avoid modifiers accidentally
overriding states. And define pseudo-classes (e.g. `:hover`) after state classes for
the same reason.

* Preprocessor nested rules should be used only when you need to reference the parent
selector (e.g. pseudo-classes, modifiers, states, etc...)

* *State* and *Modifier* classes must be tied to the selector they affect, they **should
never be declared as stand-alone rules**. Example:
    ```
    /* BAD */
    .is-active {}

    /* GOOD */
    .navbar-nav-item.is-active {}

    /* BETTER */
    .navbar-nav-item {
        &.is-active {}
    }
    ```

* Classes with the same level of indentation are considered siblings. A class "B" indented
one level more that a class "A" must be considered a child and in the markup should be nested
inside "A", example:
    ```
    // CSS
    .A {}
        .B {}

    // HTML
    <div class="A">
        <div class="B"></div>
    </div>
    ```
