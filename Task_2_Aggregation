#reducer

#!/usr/bin/env python3
import sys
from collections import defaultdict

current_user = None
action_counts = defaultdict(int)

def emit_result(user, counts):
    print(f"{user}\tposts:{counts['post']}\tlikes:{counts['like']}\tcomments:{counts['comment']}\tshares:{counts['share']}")

for line in sys.stdin:
    line = line.strip()
    if not line:
        continue

    user_id, action = line.split("\t")

    if current_user and user_id != current_user:
        emit_result(current_user, action_counts)
        action_counts = defaultdict(int)

    current_user = user_id
    action_counts[action] += 1

# Emit the last user
if current_user:
    emit_result(current_user, action_counts)


reducer_code = """#!/usr/bin/env python3
import sys
from collections import defaultdict

current_user = None
action_counts = defaultdict(int)

def emit_result(user, counts):
    print(f"{user}\\tposts:{counts['post']}\\tlikes:{counts['like']}\\tcomments:{counts['comment']}\\tshares:{counts['share']}")

for line in sys.stdin:
    line = line.strip()
    if not line:
        continue

    user_id, action = line.split("\\t")

    if current_user and user_id != current_user:
        emit_result(current_user, action_counts)
        action_counts = defaultdict(int)

    current_user = user_id
    action_counts[action] += 1

if current_user:
    emit_result(current_user, action_counts)
"""

with open("reducer_task2.py", "w") as f:
    f.write(reducer_code)

!chmod +x reducer_task2.py



# Run mapper and redirect output
!cat social_media_logs.txt | python3 mapper_task2.py > mapper_output.txt

# Sort mapper output (simulates Hadoop shuffle/sort phase)
!sort mapper_output.txt > sorted_mapper_output.txt

# Run reducer and save final output
!cat sorted_mapper_output.txt | python3 reducer_task2.py > reducer_output.txt
