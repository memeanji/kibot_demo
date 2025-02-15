# kibot_demo
import streamlit as st
from streamlit_chat import message
import re

# 챗봇 헤더
st.header("🐣 KIBOT")

# 세션 상태 초기화
if 'generated' not in st.session_state:
    st.session_state['generated'] = []  # 챗봇의 응답 기록
if 'past' not in st.session_state:
    st.session_state['past'] = []  # 사용자의 입력 기록
if 'first_message' not in st.session_state:
    st.session_state['first_message'] = True  # 첫 메시지 여부 체크

# 첫 환영 메시지
if st.session_state['first_message']:
    welcome_message = "안녕하세요! 😊 저는 라키비움의 소개를 도와줄 KIBOT🐣이에요.\n이 공간에 대해 궁금한 게 있다면 질문해 주세요!"
    st.session_state['generated'].append(welcome_message)
    st.session_state['past'].append(" ")  # 빈 문자열로 자리 유지
    st.session_state['first_message'] = False

import re

# 사용자 입력을 받아 처리하는 함수
def get_response(user_input):
    user_input = user_input.lower()  # 사용자 입력을 소문자로 변환

    # 황다인 관련
    if re.search(r"황다인|다인|다인cp|황다인 cp", user_input):
        response = "다인 CP님은 FC 콘텐츠 개발3cell에서 동계 연수 중이에요.\n저희 팀에서 디자인 담당을 하고 있어요 🖌️"
    
    # 김다영 관련
    elif re.search(r"김다영|다영|다영cp|김다영 cp", user_input):
        response = "다영 CP님은 영어 3cell에서 동계 연수 중이에요.\n저희 팀에서 도슨트 및 발표 담당을 하고 있어요 🎙️"
    
    # 조지훈 관련
    elif re.search(r"조지훈|지훈|지훈cp|조지훈 cp", user_input):
        response = "지훈 CP님은 사회 3cell에서 동계 연수 중이에요.\n저희 팀에서 문학관 참여형 콘텐츠를 담당하고 있어요 🖌️"
    
    # 윤예서 관련
    elif re.search(r"윤예서|예서|예서cp|윤예서 cp", user_input):
        response = "예서 CP님은 국어5cell에서 동계 연수 중이에요.\n저희 팀에서 도슨트 및 발표를 담당하고 있어요 🎙️"
    
    # 김민지 관련
    elif re.search(r"김민지|민지|민지cp|김민지 cp", user_input):
        response = "민지 CP님은 FC 콘텐츠 개발 3cell에서 동계 연수 중이에요.\n저희 팀의 팀장이자 ChatBot 구현담당하고 있어요 🤖"
    
    # 팀원 관련
    elif re.search(r"팀원", user_input):
        response = """
    **팀원 목록**: 👥

    1. FC 콘텐츠 개발: 김민지, 황다인  
    2. 국어 Cell: 윤예서  
    3. 사회 Cell: 조지훈  
    4. 영어 Cell: 김다영  

    저희 팀은 라키비움 공간의 다양한 부분을 담당하며,  
    서로 협력하여 프로젝트를 진행하고 있습니다.💪
    """
    
    # 책가도 관련
    elif re.search(r"책가도|책가도가 뭐야|책가도에 대해 알려줘|책가도 설명", user_input):
        response = """
    **책가도**란, 전시 초입에 위치한 책가의 모델로,  
    책과 도자기, 향로, 꽃 등이 책장 안에 놓인 모습을 그린 조선시대 그림입니다.  
    이 그림은 책을 사랑했던 선조들의 마음을 담고 있습니다. 📚

    비상 라키비움은 책가도의 형식을 차용하여,  
    전시 공간을 절제되고 모던한 책가도로 디자인하였습니다.  
    이를 통해, 비상교육의 책에 대한 진정성과 교과서에 대한 전문성을 확인할 수 있습니다.  

    이 전시 공간은 우리가 책을 어떻게 사랑하고, 전통을 어떻게 현대적으로 재해석할 수 있는지를 보여줍니다🎨
    """
    
    # 라키비움 관련
    elif re.search(r"라키비움", user_input):
        response = """
    라키비움은 '도서관'(Library), '수장고'(Archives), '박물관'(Museum)의 합성어로,  
    통합적인 공간을 상징하는 단어입니다. 🏛️

    비상 라키비움은 한글과 함께 성장한 교과서의 역사와,  
    그 교과서와 함께한 우리 문학 작품들을 총망라한 공간입니다.  
    이 공간은 우리가 어떻게 교과서를 통해 문화적 유산을 보존하고,  
    그것을 현대적인 방식으로 재해석할 수 있는지를 보여줍니다. 📚✨
    """
    
    # 이름 질문
    elif re.search(r"이름", user_input):
        response = "🐣 KIBOT이야"
    
    # 나이 질문
    elif re.search(r"나이|몇살이야|몇살|나이가 어떻게 돼?", user_input):
        response = "나는 3살이야 ! 🐣" 
    
    # 알 수 없는 명령
    else:
        response = "알 수 없는 명령입니다. 다시 입력해 주세요."
    
    return response  # return 문은 반드시 함수 내부에 있어야 합니다.

st.write(
    """
    <style>
    .chat-container {
        background-color: white;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
    }
    
    .user-message {
        background-color: #FFFACD;
        padding: 10px;
        margin-bottom: 10px;
        border-radius: 20px;
        max-width: 75%;
        margin-left: auto;
        margin-right: 0;
        display: flex;
        align-items: center;
    }

    .chatbot-message {
        background-color: white;
        border: 2px solid #FDF5D2;
        padding: 10px;
        margin-bottom: 10px;
        border-radius: 10px;
        max-width: 75%;
        margin-left: 0;
        margin-right: auto;
        display: flex;
        align-items: center;
    }

    .user-name {
        font-weight: bold;
        color: #4CAF50;
        margin-right: 10px;
    }

    .chatbot-name {
        font-weight: bold;
        color: #FF8C00;
        margin-right: 10px;
    }

    .user-message img {
        width: 30px;
        height: 30px;
        border-radius: 50%;
        margin-right: 10px;
    }

    .chatbot-message img {
        width: 30px;
        height: 30px;
        border-radius: 50%;
        margin-left: 10px;
    }
    </style>
    """,
    unsafe_allow_html=True
)

# 대화 창 표시 (최신 메시지가 아래로 오도록 정렬)
st.markdown('<div class="chat-container">', unsafe_allow_html=True)
if st.session_state['generated']:
    for i in range(len(st.session_state['generated'])):
        # 사용자 메시지와 봇의 응답을 처리
        st.markdown(f'<div class="message user">{st.session_state["past"][i]}</div>', unsafe_allow_html=True)
        st.markdown(f'<div class="message bot">{st.session_state["generated"][i]}</div>', unsafe_allow_html=True)
st.markdown('</div>', unsafe_allow_html=True)

# 입력 창을 하단에 고정
with st.form(key='chat_form', clear_on_submit=True):
    user_input = st.text_input("메시지를 입력하세요:", "", key="input")
    submitted = st.form_submit_button("Send")

# 사용자가 메시지를 보낸 경우 처리
if submitted and user_input:
    # 사용자 메시지 처리
    response = get_response(user_input)
    
    # 대화 기록 업데이트
    st.session_state.past.append(user_input)
    st.session_state.generated.append(response)

    # 페이지 새로고침 효과를 위해 rerun
    st.rerun()
