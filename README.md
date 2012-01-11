This project contains two scripts intended to be used as git pre-commit hooks.

The first, fmt-check, prevents you from committing if you need to run gofmt on any
modified .go file.

The second, fmt-fix, runs all modified .go files through gofmt before committing.
NOTE: This script does not play well when adding partial changes, such as with
`git add -p` or `git commit -p`.

You should use either one or the other, not both.

Both scripts are originally based on a [golang-nuts discussion][1].

To install in a single repository, copy a script to .git/hooks/pre-commit and make
sure it's executable.

You might also find it useful to create a git alias for gofmt by running:

    git config --global alias.gofmt '!gofmt -w `git diff --name-only --cached --diff-filter=AM | grep "\.go$"`'

Then you can run git gofmt and format all modified .go files. Note that this alias
will not handle situations where partial file changes have been added to the index.

[1]: http://groups.google.com/group/golang-nuts/browse_thread/thread/bcd1b0e3c75c3884/5ce342b06ea29d03
