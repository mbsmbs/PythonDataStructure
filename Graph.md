# Graph
  - 연결 데이터를 저장할 수 있는 자료 구조 (연결 관계)
  - 노드 : 그래프에서 하나의 데이터 단위를 나타내는 객체
  - 엣지 : 그래프에서 두 노드의 데이터를 연결
  - 인접 : 두 노드 사이에 엣지가 있을때
    - 방향 그래프 : 엣지들이 방향을 갖는다
    - 가중치 그래프 : 두 노드들을 잇는 엣지에 수치가 있다
  - 차수 : 하나의 노드에 연결되어 있는 엣지의 수 
    - 무방향 그래프 : 하나의 노드에 연결된 엣지의 수
    - 방향 그래프 : 하나의 노드의 출력 차수와 입력 차수
  - 경로 : 한 노드에서 다른 노드까지의 길
    - 비가중치 그래프 : 한 경로에 있는 엣지의 수
    - 가중치 그래프 : 한 경로에 있는 엣지의 가중치 합
    - 최단 경로 : 두 노드 사이에 가장 짧은 경로
    - 싸이클 : 한 노드에서 출발해서 다시 그 노드로 돌아오는 경우
  - 그래프 만들기:
    - 그래프 노드 클래스
    - 동적 배열 방식 & 해시 테이블 방식
    
  ## 그래프 노드 구현:
  ```
  class StationNode:
    """간단한 지하철 역 노드 클래스"""
    def __init__(self, station_name):
        self.station_name = station_name
        
    def create_station_nodes(input_file):
        """input_file에서 데이터를 읽어 와서 지하철 그래프 노드들을 리턴하는 함수"""
        stations = {}  # 지하철 역 노드들을 담을 딕셔너리

        # 파라미터로 받은 input_file 파일을 연다
        with open(input_file) as stations_raw_file:
            for line in stations_raw_file:  # 파일을 한 줄씩 받아온다
                subway_line = line.strip().split("-")  # 앞 뒤 띄어쓰기를 없애고 "-"를 기준점으로 데이터를 나눈다

                for name in subway_line:
                    station_name = name.strip()  # 앞 뒤 띄어쓰기 없애기

                    # 지하철 역 이름이 이미 저장한 key 인지 확인
                    if station_name not in stations:
                        current_station = StationNode(station_name)  # 새로운 인스턴스를 생성하고
                        stations[station_name] = current_station  # dictionary에 역 이름은 key로, 역 노드 인스턴스를 value로 저장한다

        return stations

    stations = create_station_nodes("./stations.txt")  # stations.txt 파일로 그래프 노드들을 만든다

    # stations에 저장한 역들 이름 출력 (체점을 위해 역 이름 순서대로 출력)
    for station in sorted(stations.keys()):
        print(stations[station].station_name)
  ```
  
  ### txt file
  ```
  소요산 - 동두천 - 보산 -  동두천중앙 - 지행 -  덕정 -  덕계 -  양주 -  녹양 -  가능 -  의정부 - 회룡 -  망월사 - 도봉산 - 도봉 -  방학 -  창동 -  녹천 -  월계 -  성북 -  석계 -  신이문 - 외대앞 - 회기 -  청량리 - 제기동 - 신설동 - 동묘앞 - 동대문 - 종로5가 -  종로3가 -  종각 -  시청 -  서울역 - 남영 -  용산 -  노량진 - 대방 -  신길 -  영등포 - 신도림 - 구로 -  구일 -  개봉 -  오류동 - 온수 -  역곡 -  소사 -  부천 -  중동 -  송내 -  부개 -  부평 -  백운 -  동암 -  간석 -  주안 -  도화 -  제물포 - 도원 -  동인천 - 인천 -  광명 -  가산디지털단지 - 독산 -  금천구청 -  석수 -  관악 -  안양 -  명학 -  금정 -  군포 -  당정 -  의왕 -  성균관대 -  화서 -  수원 -  세류 -  병점 -  세마 -  오산대 - 오산 -  진위 -  송탄 -  서정리 - 지제 -  평택 -  성환 - 직산 - 두정 -  천안 -  봉명 -  쌍용 -  아산 -  배방 -  온양온천 -  신창 -  서동탄
시청 -  을지로입구 - 을지로3가 - 을지로4가 - 동대문역사문화공원 - 신당 -  상왕십리 -  왕십리 - 한양대 - 뚝섬 -  성수 -  건대입구 -  구의 - 강변 - 잠실나루 -  잠실 -  신천 -  종합운동장 - 삼성 -  선릉 -  역삼 -  강남 -  교대 -  서초 -  방배 -  사당 -  낙성대 - 서울대입구 - 봉천 -  신림 - 신대방 -  구로디지털단지 - 대림 -  신도림 - 문래 -  영등포구청 - 당산 -  합정 -  홍대입구 -  신촌 -  이대 -  아현 -  충정로 - 시청
신도림 - 도림천 - 양천구청 -  신정네거리 - 까치산
신설동 - 용두 - 신답 - 용답 - 성수
대화 -  주엽 -  정발산 - 마두 -  백석 -  대곡 -  화정 -  원당 -  삼송 -  지축 -  구파발 - 연신내 - 불광 -  녹번 -  홍제 -  무악재 - 독립문 - 경복궁 - 안국 -  종로3가 -  을지로3가 - 충무로 - 동대입구 -  약수 -  금호 -  옥수 -  압구정 - 신사 -  잠원 -  고속터미널 - 교대 -  남부터미널 - 양재 -  매봉 -  도곡 -  대치 -  학여울 - 대청 -  일원 -  수서 -  가락시장 -  경찰병원 -  오금
당고개 - 상계 -  노원 -  창동 -  쌍문 -  수유 -  미아 -  미아삼거리 - 길음 -  성신여대입구 -  한성대입구 - 혜화 -  동대문 - 동대문역사문화공원 - 충무로 - 명동 -  회현 -  서울역 - 숙대입구 -  삼각지 - 신용산 - 이촌 -  동작 -  이수 -  사당 -  남태령 - 선바위 - 경마공원 -  대공원 - 과천 -  정부과천청사 -  인덕원 - 평촌 -  범계 -  금정 -  산본 -  수리산 - 대야미 - 반월 -  상록수 - 한대앞 - 중앙 -  고잔 -  공단 -  안산 -  신길온천 -  정왕 - 오이도
방화 -  개화산 - 김포공항 -  송정 -  마곡 -  발산 -  우장산 - 화곡 -  까치산 - 신정 -  목동 -  오목교 - 양평 -  영등포구청 - 영등포시장 - 신길 - 여의도 -  여의나루 -  마포 -  공덕 -  애오개 - 충정로 - 서대문 - 광화문 - 종로3가 -  을지로4가 - 동대문역사문화공원 - 청구 -  신금호 - 행당 -  왕십리 - 마장 -  답십리 - 장한평 - 군자 -  아차산 - 광나루 - 천호 -  강동 -  길동 -  굽은다리 -  명일 -  고덕 -  상일동 - 둔촌동 - 올림픽공원 - 방이 -  오금 -  개롱 -  거여 -  마천
응암 -  역촌 -  불광 -  독바위 - 연신내 - 구산 -  응암 -  새절 -  증산 -  디지털미디어시티 -  월드컵경기장 -  마포구청 -  망원 -  합정 -  상수 -  광흥창 - 대흥 -  공덕 -  효창공원앞 - 삼각지 - 녹사평 - 이태원 - 한강진 - 버티고개 -  약수 -  청구 -  신당 -  동묘앞 - 창신 -  보문 -  안암 -  고려대 - 월곡 -  상월곡 - 돌곶이 - 석계 -  태릉입구 -  화랑대 - 봉화산
장암 -  도봉산 - 수락산 - 마들 -  노원 -  중계 -  하계 -  공릉 -  태릉입구 -  먹골 -  중화 -  상봉 -  면목 -  사가정 - 용마산 - 중곡 -  군자 -  어린이대공원 -  건대입구 -  뚝섬유원지 - 청담 -  강남구청 -  학동 -  논현 -  반포 -  고속터미널 - 내방 -  이수 -  남성 -  숭실대입구 - 상도 -  장승배기 - 신대방삼거리 - 보라매 - 신풍 -  대림 -  남구로 - 가산디지털단지 - 철산 -  광명사거리 - 천왕 -  온수 -  까치울 - 부천종합운동장 - 춘의 -  신중동 - 부천시청 -  상동 -  삼산체육관 - 굴포천 - 부평구청
암사 -  천호 -  강동구청 -  몽촌토성 -  잠실 -  석촌 -  송파 -  가락시장 -  문정 -  장지 -  복정 -  산성 -  남한산성입구 -  단대오거리 - 신흥 -  수진 - 모란
개화 -  김포공항 -  공항시장 -  신방화 - 양천향교 -  가양 -  증미 -  등촌 -  염창 -  신목동 - 선유도 - 당산 -  국회의사당 - 여의도 - 샛강 -  노량진 - 노들 -  흑석 -  동작 -  구반포 - 신반포 - 고속터미널 - 사평 -  신논현 - 언주 -  선정릉 - 삼성중앙 -  봉은사 - 종합운동장
왕십리 - 서울숲 - 압구정로데오 -  강남구청 -  선정릉 - 선릉 -  한티 -  도곡 -  구룡 -  개포동 - 대모산입구 - 수서 -  복정 -  경원대 - 태평 -  모란 -  야탑 -  이매 -  서현 -  수내 -  정자 -  미금 -  오리 -  죽전 -  보정 -  구성 -  신갈 -  기흥 -  상갈 -  청명 -  영통 -  망포
용문 -  원덕 -  양평 -  오빈 -  아신 -  국수 -  신원 -  양수 -  운길산 - 팔당 -  도심 -  덕소 -  양정 -  도농 -  구리 -  양원 -  망우 -  상봉 -  중랑 -  회기 -  청량리 - 왕십리 - 응봉 -  옥수 -  한남 -  서빙고 - 이촌 -  용산 -  서울역 - 신촌 (경의중앙선) -  공덕 -  서강 -  홍대입구 -  가좌 -  디지털미디어시티 -  수색 - 화전 - 행신 -  능곡 -  대곡 -  곡산 -  백마 -  풍산 -  일산 -  탄현 -  운정 -  금릉 -  금촌 -  월롱 -  파주 -  문산
서울역 - 공덕 -  홍대입구 -  디지털미디어시티 -  김포공항 -  계양 -  검암 -  운서 -  공항화물청사 -  인천국제공항
계양 -  귤현 -  박촌 -  임학 -  계산 -  경인교대입구 -  작전 -  갈산 -  부평구청 -  부평시장 -  부평 -  동수 -  부평삼거리 - 간석오거리 - 인천시청 - 예술회관 - 인천터미널 - 문학경기장 - 선학 -  신연수 - 원인재 - 동춘 -  동막 -  캠퍼스타운 - 테크노파크 - 지식정보단지 -  인천대입구 - 센트럴파크 - 국제업무지구
상봉 -  망우 -  갈매 -  별내역 - 퇴계원 - 사릉 -  금곡 -  평내호평 -  마석 -  대성리 - 청평 -  상천 -  가평 -  굴봉산 - 백양리 - 강촌 -  김유정 - 남춘천 - 춘천
오이도 - 월곶 -  소래포구 -  인천논현 -  호구포 - 남동인더스파크 - 원인재 - 연수 -  송도
강남 -  양재 -  양재시민의숲 -  청계산입구 - 판교 -  정자
  ```
  
  ## 엣지 구현:
    - 입접 행렬:
      - 각 노드를 리스트에 저장해 고유 정수 인덱스를 준다
      - (노드 수 X 노드 수) 크기의 행렬을 만든다
      - 노드들의 엣지 유뮤 및 가중치에 따라 행렬의 요소를 채운다
  ```
  # 모든 요소를 0으로 초기화시킨 크기 6 x 6 인접 행렬
  adjacency_matrix = [[0 for i in range(6)] for i in range(6)]

  # 코드를 쓰세요
  # 엣지 (영훈, 현승) 저장
  adjacency_matrix[0][1] = 1
  adjacency_matrix[1][0] = 1

  # 엣지 (영훈, 동욱) 저장
  adjacency_matrix[0][2] = 1
  adjacency_matrix[2][0] = 1

  # 엣지 (현승, 소원) 저장
  adjacency_matrix[1][5] = 1
  adjacency_matrix[5][1] = 1

  # 엣지 (현승, 지웅) 저장
  adjacency_matrix[1][3] = 1
  adjacency_matrix[3][1] = 1

  # 엣지 (동욱, 소원) 저장
  adjacency_matrix[2][5] = 1
  adjacency_matrix[5][2] = 1

  # 엣지 (지웅, 소원) 저장
  adjacency_matrix[3][5] = 1
  adjacency_matrix[5][3] = 1

  # 엣지 (지웅, 규리) 저장
  adjacency_matrix[3][4] = 1
  adjacency_matrix[4][3] = 1

  # 엣지 (규리, 소원) 저장
  adjacency_matrix[4][5] = 1
  adjacency_matrix[5][4] = 1

  print(adjacency_matrix)
  ```

  - 인접 리스트: 각 노드의 엣지를 리스트에 저장하는 방법
  ```
  class StationNode:
    """간단한 지하철 역 노드 클래스"""
    def __init__(self, station_name):
        self.station_name = station_name
        self.adjacent_stations = []  # 인접 리스트


    def add_connection(self, other_station):
        """지하철 역 노드 사이 엣지 저장하기"""
        self.adjacent_stations.append(other_station)
        other_station.adjacent_stations.append(self)


    def __str__(self):
        """지하철 노드 문자열 메소드. 지하철 역 이름과 연결된 역들을 모두 출력해준다"""
        res_str = f"{self.station_name}: "  # 리턴할 문자열

        # 리턴할 문자열에 인접한 역 이름들 저장
        for station in self.adjacent_stations:
            res_str += f"{station.station_name} "

        return res_str
        

  def create_subway_graph(input_file):
      """input_file에서 데이터를 읽어 와서 지하철 그래프를 리턴하는 함수"""
      stations = {}  # 지하철 역 노드들을 담을 딕셔너리

      # 파라미터로 받은 input_file 파일을 연다
      with open(input_file) as stations_raw_file:
          for line in stations_raw_file:  # 파일을 한 줄씩 받아온다
              subway_line = line.strip().split("-")  # 앞 뒤 띄어쓰기를 없애고 "-"를 기준점으로 데이터를 나눈다

              for name in subway_line:
                  station_name = name.strip()  # 앞 뒤 띄어쓰기 없애기

                  # 지하철 역 이름이 이미 저장한 key 인지 확인
                  if station_name not in stations:
                      current_station = StationNode(station_name)  # 새로운 인스턴스를 생성하고
                      stations[station_name] = current_station  # dictionary에 역 이름은 key로, 역 노드 인스턴스를 value로 저장한다

      return stations


  stations = create_subway_graph("./stations.txt")  # stations.txt 파일로 그래프를 만든다

  # stations에 저장한 역 인접 역들 출력 (체점을 위해 역 이름 순서대로 출력)
  for station in sorted(stations.keys()):
          print(stations[station])       
  ```

  - V : 그래프 안에 있는 모든 노드들의 집합. 그래프 노드 = Vertex
  - E : 그래프 안에 있는 모든 엣지들의 집합.
  - V & E 관계 : E는 최악의 경우 V<sup>2</sup>에 비례
  
  - 노드를 저장하는 공간 : 인접 행렬 & 인접 리스트 이든 : O(V)
  - 인접행렬이 차지하는 공간 : O(V<sup>2</sup>)
  - 인접 리스트가 차지하는 공간 : O(V) + O(E) = O(V+E)     최악의 경우 : O(V<sup>2</sup>)
  
  - 두 노드가 연결 됐는지 확인하는 시간 : 
    - 인접 행렬 : O(1)
    - 인접 리스트 : O(V)

## 그래프 탐색
  - 하나의 시작점 노드에서 연결된 노드들을 모두 찾는 것
  - Breadth First Search (BFS) : 너비 우선 탐색
    - 중요한 추상 자료형 : 큐
    
    - 시작 노드를 방문하고  표시한 후, 큐에 넣음
    - // 큐에 아무 노드가 없을 때까지 반복 :
    - 큐 맨 앞 노드를 꺼낸다
    - 꺼낸 노드에 인접한 노드들을 모두 보면서 : 처음 방문한 노드면 : 방문 표시 후 큐에 삽입
  ```
  class StationNode:
    """지하철 역을 나타내는 역"""
    def __init__(self, station_name):
        self.station_name = station_name
        self.adjacent_stations = []
        self.visited = False

    def add_connection(self, station):
        """파라미터로 받은 역과 엣지를 만들어주는 메소드"""
        self.adjacent_stations.append(station)
        station.adjacent_stations.append(self)


    def create_station_graph(input_file):
        stations = {}

        # 일반 텍스트 파일을 여는 코드
        with open(input_file) as stations_raw_file:
            for line in stations_raw_file:  # 파일을 한 줄씩 받아온다
                previous_station = None  # 엣지를 저장하기 위한 변수
                raw_data = line.strip().split("-")

                for name in raw_data:
                    station_name = name.strip()

                    if station_name not in stations:
                        current_station = StationNode(station_name)
                        stations[station_name] = current_station

                    else:
                        current_station = stations[station_name]

                    if previous_station is not None:
                        current_station.add_connection(previous_station)

                    previous_station = current_station

        return stations
  ```
  ```
  from collections import deque
  from subway_graph import create_station_graph

  def bfs(graph, start_node):
      """시작 노드에서 bfs를 실행하는 함수"""
      queue = deque()  # 빈 큐 생성

      # 일단 모든 노드를 방문하지 않은 노드로 표시
      for station_node in graph.values():
          station_node.visited = False

      # 시작점 노드를 방문 표시한 후 큐에 넣어준다
      start_node.visited = True
      queue.append(start_node)

      while queue:  # 큐에 노드가 있을 때까지
          current_station = queue.popleft()  # 큐의 가장 앞 데이터를 갖고 온다
          for neighbor in current_station.adjacent_stations:  # 인접한 노드를 돌면서
              if not neighbor.visited:  # 방문하지 않은 노드면
                  neighbor.visited = True  # 방문 표시를 하고
                  queue.append(neighbor)  # 큐에 넣는다


  stations = create_station_graph("./new_stations.txt")  # stations.txt 파일로 그래프를 만든다

  gangnam_station = stations["강남"]

  # 강남역과 경로를 통해 연결된 모든 노드를 탐색
  bfs(stations, gangnam_station)

  # 강남역과 서울 지하철 역들이 연결됐는지 확인
  print(stations["강동구청"].visited)
  print(stations["평촌"].visited)
  print(stations["송도"].visited)
  print(stations["개화산"].visited)

  # 강남역과 대전 지하철 역들이 연결됐는지 확인
  print(stations["반석"].visited)
  print(stations["지족"].visited)
  print(stations["노은"].visited)
  print(stations["(대전)신흥"].visited)
  ```
  
  - BFS 알고리즘 시간 복잡도 : O(2V+E) -> O(V+E)
    - 전처리 : O(V)
    - 스택에서 노드 넣고 빼기 : O(V)
    - 인접한 노드들을 도는데 걸리는 시간 : O(E)

## Depth First Search (DFS) : 깊이 우선
  - 중요한 추상 자료형 : 스택

  - 시작 노드를 스택에 넣는다는 표시 후 스택에 넣음
  - 스택에 아무 노드가 없을 때까지 :
    - 스택 가장 위 노드를 꺼낸다
    - 노드를 방문표시
    - 인접한 노드들을 모두 보면서 : 처음 방문 하거나 스택에 없으면 스택에 넣는 다는 표시 후 스택에 넣는다
      
  ```
  from collections import deque
  from subway_graph import *

  def dfs(graph, start_node):
      """최단 경로용 bfs 함수"""
      stack = deque()  # 빈 큐 생성

      # 모든 노드를 처음 보는 노드로 초기화
      for station_node in graph.values():
          station_node.visited = 0

      # 코드를 쓰세요
      start_node.visited = 1  # 시작 노드를 스택에 넣는다는 표시(옅은 회색)를 하고
      stack.append(start_node)  # 스택에 넣습니다

      while stack:  # 스택에 노드가 남아 있을 때까지
          current_node = stack.pop()  # 스택 가장 위(뒤) 데이터를 갖고 온다
          current_node.visited = 2  # 현재 노드를 방문 표시한다
          for neighbor in current_node.adjacent_stations:
              if neighbor.visited == 0:  # 처음 보는 노드들만
                  neighbor.visited = 1  # 스택에 넣는다는 표시를 하고
                  stack.append(neighbor)  # 스택에 넣습니다

  stations = create_station_graph("./new_stations.txt")  # stations.txt 파일로 그래프를 만든다

  gangnam_station = stations["강남"]

  # 강남역과 경로를 통해 연결된 모든 노드를 탐색
  dfs(stations, gangnam_station)

  # 강남역과 서울 지하철 역들 연결됐는지 확인
  print(stations["강동구청"].visited)
  print(stations["평촌"].visited)
  print(stations["송도"].visited)
  print(stations["개화산"].visited)

  # 강남역과 대전 지하철 역들 연결됐는지 확인
  print(stations["반석"].visited)
  print(stations["지족"].visited)
  print(stations["노은"].visited)
  print(stations["(대전)신흥"].visited)
  ```
  - DFS 시간 복잡도 : O(2V+E) -> O(V+E)
    - 전처리 : O(V)
    - 스택에서 노드 넣고 빼기 : O(V)
    - 인접한 노드들을 도는데 걸리는 시간 : O(E)

## 최단 경로
  ### BFS : 
    - 시작 노드를 방문 표시 후, 큐에 넣음
    - 큐에 아무 노드가 없을 때까지
    - 큐 가장 앞 노드를 꺼낸다
    - 꺼낸 노드에 인접한 노드들을 모두 보면서
    - 처음 방문한 노드면 방문했다는 표시를 해주고 
    - predecessor 변수를 큐에서 꺼낸 노드로 설정해 주고
    - 큐에 넣어준다
    
  - Backtracking : 
    - 현재 노드를 경로에 추가한다
    - 현재 노드의 predecessor로 간다
    - predecessor가 없을 때까지 위 단계들 반복
    
  ```
  from collections import deque
  from subway_graph import *

  def bfs(graph, start_node):
      """최단 경로용 bfs 함수"""
      queue = deque()  # 빈 큐 생성

      # 모든 노드를 방문하지 않은 노드로 표시, 모든 predecessor는 None으로 초기화
      for station_node in graph.values():
          station_node.visited = False
          station_node.predecessor = None

      # 시작점 노드를 방문 표시한 후 큐에 넣어준다
      start_node.visited = True
      queue.append(start_node)

      while queue:  # 큐에 노드가 있을 때까지
          current_station = queue.popleft()  # 큐의 가장 앞 데이터를 갖고 온다
          for neighbor in current_station.adjacent_stations:  # 인접한 노드를 돌면서
              if not neighbor.visited:  # 방문하지 않은 노드면
                  neighbor.visited = True  # 방문 표시를 하고
                  neighbor.predecessor = current_station  # 이 노드가 어디서 왔는지 표시 
                  queue.append(neighbor)  # 큐에 넣는다


    def back_track(destination_node):
        """최단 경로를 찾기 위한 back tracking 함수"""
        res_str = ""  # 리턴할 결과 문자열
        temp = destination_node  #  도착 노드에서 시작 노드까지 찾아가는 데 사용할 변수

        # 시작 노드까지 갈 때까지
        while temp is not None:
            res_str = f"{temp.station_name} {res_str}"  # 결과 문자열에 역 이름을 더하고
            temp = temp.predecessor  # temp를 다음 노드로 바꿔준다

        return res_str

    stations = create_station_graph("./new_stations.txt")  # stations.txt 파일로 그래프를 만든다

    bfs(stations, stations["을지로3가"])  # 지하철 그래프에서 을지로3가역을 시작 노드로 bfs 실행
    print(back_track(stations["강동구청"]))  # 을지로3가에서 강동구청역까지 최단 경로 출력
  ```

  ### Dijkstra
    - 3 가지 변수들의 역할 :
      - Distance : 특정 노드까지의 최단 거리 예상치
      - Predecessor : 현재까지 찾은 최단 경로에서 바로 직전의 노드
      - Complete : 노드까지의 최단 경로를 찾았다고 표시하기위한 변수
    - 엣지 (A, B)를 relax 한다 : 더 가까운 거리를 찾아서 업데이트를 시켜주는 것
    
    - 시작점의 Distance를 0으로, predecessor를 None으로
    - 모든 노드가 complete 일 때까지 :
    - complete하지 않은 노드 주 Distance가 가장 작은 노드 선택
    - 이 노드에 인접한 노드 중 complete하지 않은 노드를 돌면서 각 엣지를 Relax 한다
    - 현재 노드를 complete 처리한다 
    
