# loop-driver

The loop-driver contract shared by
[LedgerEvolve](https://github.com/micuintus/ledgerevolve) and
[EnforcedTodo](https://github.com/micuintus/enforced-todo): after each
agent run, a driver either stacks a follow-up turn or stays idle.

This is a library for Pi extension authors, not an extension. Users
get it automatically as a dependency.

```ts
import { attachLoopDriver } from "@micuintus/loop-driver";

export default function (pi) {
	attachLoopDriver(pi, {
		iterate(ctx, event) {
			// Return a prompt to continue, or null to stay idle.
			return null;
		},
	});
}
```

The driver does not stack a follow-up when the run was aborted, when
messages are already queued, or when the run ended on a provider error
(a rate-limited run would otherwise retry at API speed); the last case
notifies the user instead.

```sh
npm install @micuintus/loop-driver
```

Extracted with its history from `pi-dacmicu` (`packages/base`).
