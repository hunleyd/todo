# todo - a quirky little todo utility

If you've spent any time on a *NIX machine, you're probably vaguely familiar with
`pushd` and `popd`. I've had it in my head for a while now that the way these
two utilities work is 80% of a 'todo' task list manager given how I
tend to work. All that is really missing is the recording of tasks to paths to
the stored $PWD. That's where `todo` comes in :)

The workflow is basically this:
1. get interrupted and have to switch tasks
2. leave yourself a note about what you are doing before you context switch
3. go handle the interruption
4. pop the todo back off the stack

In actual practice, it looks like:
```
~/projects/foo #> todo push 'finish the new unit test'
~/projects/foo #> mkdir ../bar
~/projects/foo #> cd ../bar
~/projects/bar #> [do the needful for the interruption]
~/projects/bar #> todo pop
~/projects/foo #> # finish the new unit test
~/projects/foo #> [finish the new unit test]
```

Under the covers, `todo push` saves the current $PWD and the text of your reminder to
`~/.config/todo/tasks.lst` and then `todo pop` grabs the most recent entry,
switches to the directory associated with it, and then prints the reminder text
that you entered.

That's it. Pretty trivial. right?

Planned features:

- [✅] LIFO support
- [✅] FIFO support
- [✅] popping a task w/o removing it from the stack
- [ ] viewing the stack of reminders
- [ ] popping an arbitrary reminder off the stack

