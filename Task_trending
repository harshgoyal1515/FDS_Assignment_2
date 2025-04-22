#mapper

#!/usr/bin/env python3
import sys

# Mapper: Emits (content_id, 1) for each like or share
for line in sys.stdin:
    fields = line.strip().split("\t")
    if len(fields) != 5:
        continue

    _, _, action_type, content_id, _ = fields
    action_type = action_type.lower()

    if action_type in ["like", "share"]:
        print(f"{content_id}\t1")

with open("mapper_task3.py", "w") as f:
    f.write("""#!/usr/bin/env python3
import sys

# Mapper: Emits (content_id, 1) for each like or share
for line in sys.stdin:
    fields = line.strip().split("\\t")
    if len(fields) != 5:
        continue

    _, _, action_type, content_id, _ = fields
    action_type = action_type.lower()

    if action_type in ["like", "share"]:
        print(f"{content_id}\\t1")
""")
