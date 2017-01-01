
# Android tools
- Stetho
    * https://github.com/facebook/stetho
    * chrome browser를 이용
    * Network logging >> 네트워크 APIㅇ와의 연결은 필요  
        Okhttp StehoiInterceptor / NetworkEventReporter(소켓,암화화 등의 경우) 등 활용
    * 앱 내부 sqlite db sql 조회 수정
        - DatabaseDriver를 이용하여 다른 db도 활용 가능
    * SharedPreference도 가능 /
    * gradle 설정
        - dependencies { debugComplie 'com.facebook.stetho:stetho:1.4.1'} 
        - debugcompile을 해야함
    * 
- LeakCanary
    * https://github.com/square/leakcanary
    * http://pluu.github.io/blog/android/2015/09/11/leakcanary/
    * 앱에 그냥 넣어서 사용할 경우 onDestroy() 시점에 GC 때문에 약간의 freezing이 있을 수 있으니 사용에 주의할 것 
    * activity에 대한 memory leak만 검출 가능

- HierarchyViewer
    + device monitor에 통합되어 있으나 찾기 어려움.... 
    + 기본적으로 에뮬레이터나 루팅된 기기에서만 사용 가능
    + Android studio 2.2 : Layout Inspector 제작중

- Debugger tips
    + conditional breakpoint : break point에서 우클릭시 condition 설정 가능
    + suspend 옵션을 끄면, 빌드 없이 임시 로그 추가 가능