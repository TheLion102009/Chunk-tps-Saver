Chunk-tps-Saver
=================

Short description
-----------------
Plugin to detect and back up chunk-related TPS lag (backup + optional banning). Compatible with Paper/Folia 1.21.x.

Features
--------
- Monitors global TPS and estimates per-world TPS
- Scans loaded chunks for lag factors (entities, tile entities, redstone indicators)
- Creates backup snapshots of suspicious chunks: plugins/ChunkTpsSaver/backups/<world>/<x>_<z>.nbt
- Regenerates problematic chunks (currently: replaces chunk blocks with AIR as a fallback)
- Optional automatic ban of players standing in problematic chunks (configurable)

Installation
------------
1. Copy the JAR (build/libs/Chunk-tps-Saver-0.1.jar) into the server's plugins folder.
2. Restart the server (Paper or Folia, Minecraft 1.21.x).
3. Edit plugins/ChunkTps-Saver/config.yml and reload the plugin.

Config (main options)
---------------------
- thresholdTps: global TPS threshold below which a scan starts (default 10.0)
- checkIntervalSeconds: interval in seconds to check the threshold (default 5)
- chunkScoreThreshold: score at which a chunk is considered suspicious (default 50)
- banDurationHours: ban duration in hours. -1 = permanent, 0 = no ban, >0 = temporary in hours (default 0)

Backup path
-----------
Backups are stored as YAML snapshots with a .nbt extension:
plugins/ChunkTpsSaver/backups/<world>/<x>_<z>.nbt
Note: This is not a native Anvil/Region NBT backup but a block/tile-entity snapshot. A restore command is implemented that reads these snapshots.

Safety & notes
--------------
- Scanning and writing full chunks is expensive and can itself cause load; test on a staging server first.
- By default the plugin creates a backup before any destructive action. Automatic deletion/ban is configurable — use with caution.
- Current regeneration is a simple fallback that sets all chunk blocks to AIR. Consider replacing this with a proper region restore for production.

Troubleshooting
---------------
- Build: use the Gradle wrapper: ./gradlew clean build. The built JAR appears in build/libs.
- If kick/ban APIs change, the plugin can be adapted to component-based kick messages or native ban APIs.

Roadmap / suggestions
---------------------
- Better restore: real region/Anvil backups instead of YAML snapshots
- Admin whitelist/confirm mode instead of immediate ban/delete
- Further scan optimizations: asynchronous sampling, chunk batching
- Replace deprecated kick method with Component API

Contact
-------
If you want additional features (restore improvements, whitelist changes, async scan), tell me which and I will implement them.

License
-------
MIT (or specify another license if you prefer)
