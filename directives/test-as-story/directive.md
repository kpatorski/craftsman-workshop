---
id: test-as-story
title: Structure every test as given / when / then
description: >
  The body reads like prose. Use Spock's native given/when/then labels, or //given //when //then comments where the framework has none (JUnit). Each block is one or two intent-revealing calls, not a wall of setup. Stubbing and object building move into small helpers named in human language.
applies-when: writing the body of a test
precedence: the project's existing test structure wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

Must:

- every test has explicit given / when / then blocks
- no inline mock wiring in the body when a named helper reads better

## Examples

    void userIsNotCreatedIfUsernameIsAlreadyTaken() {
        // given existing users
        var userRepository = addUsersToRepository(user("user-a"), user("user-b"));

        // when create user of existing username
        var newUser = new CreateUser(userRepository).handle(command("user-b"));

        // then new user is not created
        assertTrue(newUser.isEmpty());
    }
