# How a review checks each directive

The review reads this table, never the directives themselves, to decide where each directive it checks goes. The
directives say how code is written and know nothing of the review; this table is the review's own reading of them.

- `Files` — the changed files the directive is checked on:
  - `production` — every changed file that is not a test;
  - `tests` — the test files: in a `test`, `tests` or `__tests__` folder, or named as a test (`*Test.*`, `*Tests.*`,
    `*Spec.*`, `*.test.*`, `*.spec.*`, `test_*.py`);
  - `all` — every changed file;
  - `none` — not checked in a review: it is about writing specs or commits, or it only gathers other directives that
    have rows of their own.
- `Reach` — what a reviewer needs to see:
  - `file` — one file is enough to judge it (a name, a comment, a method's exits, who uses a class it makes public). It
    is checked once over the whole change, the files in batches; the reviewer looks up in the code whatever else the
    file's code relies on.
  - `flow` — it needs the use case: what calls what, across files and modules. It is checked per use case.

A directive with no row here is checked on `all` files with `flow` reach, and the review page and the dashboard name
it, so a row can be added.

| Directive                        | Files      | Reach |
|----------------------------------|------------|-------|
| `abstraction-timing`             | production | file  |
| `aggregate-design`               | production | flow  |
| `architecture-profile`           | production | flow  |
| `commit-message`                 | none       | -     |
| `crud-or-domain`                 | none       | -     |
| `defer-discovered-gaps`          | none       | -     |
| `determinism`                    | production | file  |
| `error-handling`                 | production | file  |
| `feature-structure`              | production | flow  |
| `framework-isolation`            | production | flow  |
| `functional-style`               | production | file  |
| `interfaces`                     | production | file  |
| `libraries-first`                | all        | file  |
| `logging`                        | production | file  |
| `method-exits`                   | production | file  |
| `module-dependencies`            | production | flow  |
| `naming`                         | production | file  |
| `no-explanatory-comments`        | all        | file  |
| `prefer-assertj-under-junit`     | tests      | file  |
| `prefer-liquibase-owned-schema`  | production | flow  |
| `prefer-lombok`                  | production | file  |
| `prefer-mockito-under-junit`     | tests      | file  |
| `prefer-result-type-library`     | production | file  |
| `prefer-spock`                   | tests      | file  |
| `prefer-spock-mocks`             | tests      | file  |
| `prefer-testcontainers-postgres` | tests      | file  |
| `production-code`                | none       | -     |
| `readme`                         | all        | file  |
| `rich-domain`                    | production | flow  |
| `security`                       | production | flow  |
| `simplest-solution`              | production | flow  |
| `single-responsibility`          | production | file  |
| `specifications`                 | production | file  |
| `type-contracts`                 | production | file  |
| `value-objects`                  | production | file  |
| `visibility`                     | production | file  |
| `acceptance-criteria-format`     | none       | -     |
| `classify-task-shape`            | none       | -     |
| `definition-of-done`             | none       | -     |
| `dependencies-explicit`          | none       | -     |
| `no-invented-requirements`       | none       | -     |
| `one-task-granularity`           | none       | -     |
| `spec-rules`                     | none       | -     |
| `dummy-values`                   | tests      | file  |
| `how-high-to-test`               | tests      | flow  |
| `stub-vs-in-memory`              | tests      | file  |
| `suite-layout`                   | tests      | file  |
| `test-as-story`                  | tests      | file  |
| `test-data`                      | tests      | flow  |
| `test-fixtures`                  | tests      | flow  |
| `test-naming`                    | tests      | file  |
| `test-style`                     | tests      | file  |
