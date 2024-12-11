# C++/WinRT
C++/WinRT를 사용하여 XAML 컨트롤 빌드
새 항목 추가를 선택합니다. Visual C++->WinUI 아래에서 사용자 지정 컨트롤(WinUI) 템플릿을 선택합니다. 새 컨트롤의 이름을 "BgLabelControl"로 지정하고, 추가를 클릭합니다.
BgLabelControl.h는 컨트롤 선언을 포함하는 헤더이고, BgLabelControl.cpp는 컨트롤의 C++/WinRT 구현을 포함합니다. BgLabelControl.idl은 컨트롤을 런타임 클래스로 인스턴스화할 수 있는 인터페이스 정의 파일입니다.
런타임 클래스를 구현하도록 프로젝트 디렉터리에 있는 BgLabelControl.idl, BgLabelControl.h 및 BgLabelControl.cpp 파일의 코드를 업데이트합니다.

xaml_typename 함수는 WinUI 3 프로젝트 템플릿에 기본적으로 포함되지 않는 Windows.UI.Xaml.Interop 네임스페이스를 통해 제공됩니다. 이 네임스페이스와 연결된 헤더 파일(pch.h)을 포함하도록 프로젝트의 미리 컴파일된 헤더 파일에 줄을 추가합니다.
// pch.h
...
#include <winrt/Windows.UI.Xaml.Interop.h>
...

Generic.xaml의 기본 내용을 삭제하고, 아래 태그를 붙여넣습니다.
<!-- \Themes\Generic.xaml -->
<ResourceDictionary
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:BgLabelControlApp">

    <Style TargetType="local:BgLabelControl" >
        <Setter Property="Template">
            <Setter.Value>
                <ControlTemplate TargetType="local:BgLabelControl">
                    <Grid Width="100" Height="100" Background="{TemplateBinding Background}">
                        <TextBlock HorizontalAlignment="Center" VerticalAlignment="Center" Text="{TemplateBinding Label}"/>
                    </Grid>
                </ControlTemplate>
            </Setter.Value>
        </Setter>
    </Style>
</ResourceDictionary>

MainWindow.xaml을 엽니다. 여기에는 기본 UI 페이지에 사용할 XAML 태그가 포함되어 있습니다. StackPanel 내부에서 Button 요소 바로 뒤에 다음 태그를 추가합니다.
<local:BgLabelControl Background="Red" Label="Hello, World!"/>

MainWindow 형식(XAML 태그 및 명령적 코드 컴파일의 조합)이 BgLabelControl 템플릿 컨트롤 형식을 인식하도록 다음 include 지시문을 MainWindow.h 추가합니다. 
//MainWindow.h
...
#include "BgLabelControl.h"
...

....

