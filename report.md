


The `data/` folder stores the generated YAML configuration files per cluster. For example, under `data/iac2/`, we have two main folders:

- `latest/`: this always contains the most recent snapshot for each flow, so it is easy to check the current state of the cluster.
- `history/<timestamp>/`: this stores immutable snapshots for each scale run. Every time we run the export again, a new timestamped folder is created, so we can compare different versions over time.

The `reports/` folder stores the scale test report in CSV format. Each run has one report file, including the flow name, task ID, status, elapsed time, object count, file size, output path, and error details if a flow fails.

For the latest full run on IAC2, I executed all 30 generator flows. 26 flows completed successfully and generated YAML files. 4 flows currently have issues, and I am investigating them:

- `accesspoint_location`: looks like an SDK/API compatibility issue. The generator calls `get_access_points_positions`, but the current SDK version exposes the newer `get_access_points_positions_v2`.
- `application_policy`: the YAML was generated in the artifact folder, but the MCP runner did not complete cleanly.
- `events_and_notifications`: similar case. The YAML output exists, but the runner did not return a clean completed status.
- `wired_campus_automation`: this hit unsupported device/platform or software version errors while collecting wired feature configuration.

This is useful because if one flow fails, we do not lose the results from the previous successful flows and do not need to rerun everything from scratch.

In short, the repo is now intended to be the source of record for scale export snapshots, version history, and run reports. The next step is to fix or handle the 4 problematic flows so the full 30-flow export can complete cleanly.