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
╭─doug@nuc ~/repos/todo  ‹main*›
╰─➤  ./todo push "something I need to do"
todo: Creating new todo: something I need to do
todo: You have 1 todos
<go handle the interruption>
╭─doug@nuc ~  ‹main*›
╰─➤  ~/repos/todo/todo pop
todo: something I need to do
todo: cd /home/doug/repos/todo to continue this todo
╭─doug@nuc ~/repos/todo  ‹main*›
╰─➤  ~/repos/todo/todo pop
todo: no todos remain! Congrats!!
```

Under the covers, `todo push` saves the current $PWD and the text of your reminder to
`~/.config/todo/tasks.lst` and then `todo pop` grabs the most recent entry,
tells you the directory associated with it, and then prints the reminder text
that you entered.

Note that `todo` will attempt to find en entry for the current $PWD and if there are
none, it will fall back to any task (while still respecting your LIFO/FIFO preference
in either case).

That's it. Pretty trivial. right?

Planned features:

- ✅ LIFO support
- ✅ FIFO support
- ✅ popping a task w/o removing it from the stack
- ✅ popping a task from just the current project or all projects
- ✅ viewing the stack of reminders

Configuration:

At this time, the following configuration options are available:
- PRESERVE_QUEUE - Boolean - Whether or not to remove popped tasks from the queue
- PROJECTS_ONLY - Boolean - Whether or not to look for any tasks to pop or only from the current project dir
- QUEUE_MODE - enum - Valid values are 'lifo' and 'fifo'. Determines if we should pop the oldest or newest todo
