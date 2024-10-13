# dmeditor-lang

Experiment to integrating DM Editor with languages, PHP as main.

Main goal is to make it as a PHP project's "engine for visual editing", with use cases like making compaign page visually. To achieve that, below should be supported:

- Allow PHP (or template) to include DM Editor.
- Support widget making in php template(eg. twig), which is loaded both in front site and admin editing.
- Support defining styles in config/js config
- [not here but in solution] a place to launch dmeditor & save
- [not here but in solution] asset integration, including images, files, links, data source (future).

## Approach 1: remote

Run a nextjs server behind (mostly on localhost and proxy nextjs to client).

Pros: mature platforms

Cons:

1. Need extra server to run
2. request to nextjs (embed) and request back (for widget rendering)? - maybe it's not a big deal as long as it's stable and easy to set up.

## Approach 2: native

Use php_v8js to run react for both server and client. Other languages Python: pyv8, Java: j2v8, Go: v8go.

_(PS. seems in Python community they prefere Approach 1. eg. https://github.com/markfinger/python-react)_

Props: native invoking - php invoking js and js invoking php (and template)

Cons:

1. Complex set up
2. library for rendering js in PHP (both server and client) is not proved reliable(and up to php 8 version)

## Ideas about using it in project

PHP Developer in the end can have 2 ways to develop widget:

- Most templating only, not much script: template (eg. twig)
- Templating + script: use react for script & rendering (not suggest to use template + script, they can just use graphql for data + client react )

For server choosing suggestion:

- Most of php layout / page template: use php server
- Most of widget templates (doesn't matter php template for react): use nodejs server (eg. nextjs)

## Implemtation

Sub projects:

- [dmeditor-lang](./dmeditor-lang)(js library): a dmeditor widget wrapper which loads PHP templates as widget (with styles parameter), define styles by config.
- [php](./php) (php library, symfony vendor): php wrapper for invoking DM Editor View, provding template and invoking widget rendering (for edit view).
- [sample](./sample): sample project of using php lib & dmeditor-lang.
