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
  - Example:
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
    
