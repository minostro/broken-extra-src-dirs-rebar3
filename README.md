extra_src_dirs
======

`rebar3` does not compile files that belongs to folders specified in `extra_src_dirs`.

In this repo you can find two folders:

1. broken-project:  When running `REBAR_PROFILE=test ./rebar3 compile` rebar does not include files that belongs to folders specified in `extra_src_dirs`.  The following is the rebar3 version `rebar 3.0.0-beta.4+build.3311.refcb02636 on Erlang/OTP 18 Erts 7.2`.

This is the content of `rebar.config`:

```erlang
{erl_opts, [debug_info]}.
{deps, []}.

{profiles, [
	    {test, [
		    {erl_opts, [debug_info,
		    	        {extra_src_dirs, ["test"]}]}
		   ]}
	   ]}.
```

These are the binaries after compilation:

```bash
➜  broken-extra-src-dirs-rebar3 git:(master) ✗ ls broken-project/_build/test/lib/mylib/ebin
mylib.app      mylib_app.beam mylib_sup.beam
```

2. good-project: When running `REBAR_PROFILE=test ./rebar3 compile` rebar does include files that belongs to folders specified in `extra_src_dirs`.  The following is the rebar3 version `rebar 3.0.0-alpha-6 on Erlang/OTP 18 Erts 7.2`.

This is the content of `rebar.config`:

```erlang
{erl_opts, [debug_info]}.
{deps, []}.

{profiles, [
	    {test, [
		    {extra_src_dirs, ["test"]},
		    {erl_opts, [debug_info]}
		   ]}
	   ]}.
```

These are the binaries after compilation:

```bash
➜  broken-extra-src-dirs-rebar3 git:(master) ✗ ls good-project/_build/test/lib/mylib/ebin
main_test.beam mylib.app      mylib_app.beam mylib_sup.beam
```
