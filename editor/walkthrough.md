## Apply freshness policy to a verified session

Returns [policy accepted, claims time accepted, assurance/freshness accepted, session age]. Use only after the host has authenticated and verified the issuer, audience and signature. Invalid arguments and nonfinite results return an empty vector.

1. Open an empty file named `harrier-demo.blyx`.
2. Type `blyx-harrier-demo` and select **Harrier — runnable example**. You can also use **Snippets: Fill File with Snippet**.
3. Choose **Blyx: Run File** from the command palette. Change an argument near the end of `fn main()` to try another input.

Expected output

```text
1
1
1
8
```

[Work through the example in the browser](https://www.blyx-lang.space/play?example=package-harrier)
