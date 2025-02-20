```python
   import json
   import glob
   
   # 🔹 JSON 파일 리스트 가져오기 (현재 디렉토리의 모든 JSON 파일)
   json_files = glob.glob("data/*.json")  # 'data' 폴더 내 JSON 파일을 가져옴
   
   # 🔹 데이터를 저장할 리스트 초기화
   merged_data = []
   
   # 🔹 모든 JSON 파일을 읽어서 리스트에 추가
   for file in json_files:
       with open(file, "r", encoding="utf-8") as f:
           data = json.load(f)  # JSON 파일 로드
           if isinstance(data, list):  # 데이터가 리스트 형태인지 확인
               merged_data.extend(data)  # 리스트 확장
           else:
               print(f"⚠️ {file} 파일은 리스트 형식이 아닙니다. 건너뜁니다.")
   
   # 🔹 중복 제거 (ID 기준)
   merged_data = {item["id"]: item for item in merged_data}.values()
   
   # 🔹 합친 데이터를 새로운 JSON 파일로 저장
   with open("merged_data.json", "w", encoding="utf-8") as f:
       json.dump(list(merged_data), f, ensure_ascii=False, indent=4)
   
   print(f"✅ {len(json_files)}개의 JSON 파일을 병합했습니다.")
```
