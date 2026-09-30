# snp_call_nf training materials

These are the materials from a three-hour, hands-on Nextflow session delivered
over Zoom on 29 July 2026 to colleagues in Mali. The goal was practical: by the
end of the afternoon, each learner could launch the
[snp_call_nf](https://github.com/bguo068/snp_call_nf) pipeline on a shared
server, read its outputs, diagnose a failed run from the work directory, and
recover with `-resume`. The longer-term aim was for the team to run the pipeline
comfortably on their own *P. falciparum* sequencing data.

The course is built around using a pipeline rather than writing one. Learners
never edit `main.nf`. Instead they change what the pipeline does from the
outside, through the sample sheet, command-line parameters, and configuration
files. Along the way they meet the core Nextflow ideas (processes, tasks,
channels, tuples, the work directory) by reading the output of their own runs.

The session ran on a single shared server without a job scheduler, so the
setup relies on the local executor, a small `training.config` that caps each
learner's CPU use, and a pre-built software environment that everyone shares.
Everything was staged in advance so that nobody had to install or download
anything during the session.

Preparing the course also surfaced a bug in the pipeline's early-exit options,
which was reported and fixed upstream in
[PR #22](https://github.com/bguo068/snp_call_nf/pull/22).

## What's here

- `snp_call_nf_follow_along.md` / `.pdf`: the learner guide used during the
  session
- `training.config`: per-learner resource caps and the fail-fast error
  strategy used during the session. The comments explain why the overrides
  sit inside `profiles { standard { } }`, which is the detail most likely to
  trip you up when writing your own.

## Notes on reuse

The guide was written against `snp_call_nf` commit `5386e4a` on `main`. Part 5
deliberately triggers a failure that has since been fixed upstream, so check out
that commit if you want to reproduce the session exactly.

Server hostnames and paths are placeholders. The guide assumes an instructor has
staged a shared folder containing the pipeline, its reference genomes, the
prebuilt tool environment, and `training.config`, and that sourcing `env.sh`
from that folder sets `$SNPTRAIN` to point at it. Substitute your own paths
before teaching from it.

To rebuild the PDF after editing the guide:

    pandoc snp_call_nf_follow_along.md -o snp_call_nf_follow_along.pdf --pdf-engine=xelatex --toc
