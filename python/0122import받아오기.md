import json



music_file = open('data/music.json',encoding='utf-8')   ## data라는 파일밑에 뮤직제이슨 열어줘

music_dict = json.load(music_file)

dict에 있는 키에접근하는 방식

1. [ ] 사용해서 사용하기

   singer =music_dict['singer']

   > > 만약 안에 signer없으면 오류가난다

2. get 사용하기

   album = music_dict.get('album')

   > 만약 안에 album 없으면 none을 반환해준다



def music_info(music_dict):

​	# 결과값 반화을 위한 dict

​	result{}

#인자로 들어온 musci_dict에서 내가원 하는 데이터만 추출

​	singer =music_dict['singer']

​	album = music_dict.get('album')

#결과값 dict에 데이터를 구조화

​	result['singer'] =singer          ##result = {'singer':'iu'}

​	result['album']=album

​	

​	return result

print(music_info(music_dict))



리스트라면? 시퀀스타입이기때문에 반복작업을 할수있다

def music_info(music_list):

​		result = []       ## 리스트안에 딕셔너리가 있다

​		for music in musics_list:

​				info={} ## 이걸 리줠트에 넣고싶다   result.append(info)

​			singer =music_dict.get('singer')

​			album = music_dict.get('album')

​			info['singer']  = singer

​			info['album'] = album

​			

​			#result.append(info)

​			result += [info]     ## 시퀀스타입과 시퀀스타입의 결합

​	return result

music_info(muics_list)



a= [1,2,3] + '가나다'

str와 list 연산 x



a = [1,2,3] + [가,나,다]

=[1,2,3,가,나,다]