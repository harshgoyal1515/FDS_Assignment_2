import json
from datetime import datetime

input_file = "social_media_logs.txt"
output_file = "cleansed_output.txt"
error_log = "rejected_records.txt"

# Counters
invalid_field_count = 0
invalid_timestamp = 0
invalid_json = 0
valid_records = 0

with open(input_file, "r", encoding="utf-8") as infile, \
     open(output_file, "w", encoding="utf-8") as outfile, \
     open(error_log, "w", encoding="utf-8") as errfile:

    for line in infile:
        fields = line.strip().split("\t")

        if len(fields) != 5:
            invalid_field_count += 1
            errfile.write(f"Invalid_Field_Count\t{line}")
            continue

        timestamp, user_id, action_type, content_id, metadata = fields

        # Normalize timestamp format
        timestamp_clean = timestamp.replace("T", " ").replace("Z", "")

        try:
            datetime.strptime(timestamp_clean, "%Y-%m-%d %H:%M:%S")
        except:
            invalid_timestamp += 1
            errfile.write(f"Invalid_Timestamp\t{line}")
            continue

        try:
            json.loads(metadata)
        except:
            invalid_json += 1
            errfile.write(f"Invalid_JSON\t{line}")
            continue

        valid_records += 1
        outfile.write(f"{user_id}\t{timestamp}\t{action_type}\t{content_id}\t{metadata}\n")

print("✅ Cleansing complete.")
print(f"✔ Valid records: {valid_records}")
print(f"❌ Invalid fields: {invalid_field_count}")
print(f"❌ Invalid timestamps: {invalid_timestamp}")
print(f"❌ Invalid JSON: {invalid_json}")
print(f"📄 Output file: {output_file}")
print(f"🪵 Error log file: {error_log}")
