---
title: Job Configuration
parent: Proposals
tags:
- proposals
---

# Job configuration

As tutorials are written, needs for varying levels of job
configuration are needed. This doc is meant to catalog all options on
the table for job configuration and serve as a reference for
discussion.

## Arguments

As an environment variable.

```sh
#!/bin/bash
echo ${FILENAME}
```

As a positional argument.

```sh
#!/bin/bash
echo ${1}
```

Pros:
 - Several existing scripts/binaries in the world can be dropped in.

## Destination

Hard coded.

```sh
#!/bin/bash

touch ~/destination/foo.txt
```

Pros:
 - Explicit, easy to understand workflow
 
Cons:
 - Not flexible
 - Not portable

Specified in job config.

config:
```toml
destination = "~/destination/"
```

```sh
#!/bin/bash

touch ${DESTINATION}/foo.txt
```

Pros:
 - more flexible
 - Can serve a multi-stage pipeline

Cons:
 - More files required.

