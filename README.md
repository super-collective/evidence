# Evidence

Explores approaches for storing work evidence of Polkadot Collectives in a public and transparent way. The motivation is to offer the general tokenholders an easy way to verify the work of the Collectives.

## Structure

This repo uses a relational data schema through symlinks. All evidence report file can be found in the `evidence` directory.

The information is augmented by the sub-folder `by-date` and `by-reporter`. Those allow structured access to the evidence reports without additional tooling.

The full folder structure is as follows:

```pre
- evidence
  - *.evidence # All evidence reports
  - by_date
	- 2024
	  - 01
		- 01
		  - *.evidence # Symlinks
  - by_reporter
	- alice
	  - *.evidence # Symlinks
```

## Adding Evidence

You can either manually create the `.evidence` YAML files according to the [schema] file, or use the [collective-cli] for a more stream-lined process. The command is:

```sh
collective new evidence
```

This will walk you through some fundamental questions (some of which are cached) and the creates a new evidence report file. You are still expected to fill out any remaining information manually.

To just try out the process, you can append `example` like so:

```sh
collective new evidence example
```

Be sure to configure the JSON schema into your editor to get documentation and hints about the fields. The schema can be obtained from the [collective-cli]() via:

```sh
collective schema evidence -o evidence_schema.json
```

The filename must be unique and in the form `n.evidence` for `n` being a non-negative decimal integer with at most 9 digits.

### Updating the Indices

This should be done by CI, but to manually do it you can run:  
```sh
collective index evidence
```
and may need to add `--reindex` if indexed information was changed.

<!-- LINKS -->
[collective-cli]: http://github.com/super-collective/collective-cli
[schema]: https://github.com/super-collective/collective-cli/blob/master/schema/evidence_report.json
