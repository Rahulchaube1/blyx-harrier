<img src="assets/logo.png" width="112" height="112" alt="Harrier logo">

# Harrier

Apply time and assurance policy to a session after upstream identity verification. This Blyx workflow framework is part of the audit, identity and reliability collection.

A still-valid token can represent an old or insufficiently verified session. Apply application policy after the identity provider has verified the token. [IETF RFC 7519, registered claims](https://www.rfc-editor.org/rfc/rfc7519.html#section-4.1)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-harrier.git
cd blyx-harrier
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-harrier) · [Package page](https://www.blyx-lang.space/packages/harrier) · [Handbook](https://doc.blyx-lang.space/guide/harrier)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-harrier.git vendor/harrier
```

```blyx
use vendor::harrier::harrier;

fn main() {
    let now = 100.0;
    let begins = 90.0;
    let expires = 110.0;
    let skew = 0.0;
    let observed = 2.0;
    let required = 2.0;
    let auth_time = 92.0;
    let max_age = 10.0;
    let result = harrier_session(now, begins, expires, skew, observed, required, auth_time, max_age);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
1
1
1
8
```

## API

`harrier_session(now, begins, expires, skew, observed, required, auth_time, max_age)`

Returns [policy accepted, claims time accepted, assurance/freshness accepted, session age]. Use only after the host has authenticated and verified the issuer, audience and signature. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| now | A exact signed integer |
| begins | A exact signed integer |
| expires | A exact signed integer |
| skew | A nonnegative exact integer |
| observed | A nonnegative exact integer |
| required | A nonnegative exact integer |
| auth_time | A exact signed integer |
| max_age | A nonnegative exact integer |

## Run the command-line project

Run the example with your own numbers. Vector arguments accept up to 16 comma-separated entries; use `[]` for an empty vector. The imported API accepts longer vectors. Invalid arguments return a nonzero exit status.

```sh
blyxc native-run project.blyx -- 100 90 110 0 2 2 92 10
```

## Libraries

- [ClaimClock](https://github.com/Rahulchaube1/blyx-claimclock/tree/v0.1.0) — Evaluate activation and expiration bounds on previously verified claims.
- [AssuranceLevel](https://github.com/Rahulchaube1/blyx-assurancelevel/tree/v0.1.0) — Check session freshness and an application-defined ordered assurance level.

This release includes identical copies of both library modules so a tagged clone can build offline.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-harrier/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
