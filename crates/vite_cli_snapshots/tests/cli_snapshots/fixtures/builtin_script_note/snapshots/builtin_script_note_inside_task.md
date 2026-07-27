# builtin_script_note_inside_task

## `vp run wrapped-dev`

no note: a task-spawned `vp dev` is already on the script path

**Exit code:** 1

```
$ vpt pipe-stdin ignored -- vp dev --port 12312312312 ⊘ cache disabled
error when starting dev server:
Error: No available ports found between 12312312312 and 65535
```
