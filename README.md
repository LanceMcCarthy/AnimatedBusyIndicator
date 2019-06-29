# AnimatedBusyIndicator
A UWP control leveraging WinUI and Composition

![Demo GIF](https://dvlup.blob.core.windows.net/general-app-files/GIFs/AnimatedBusyIndicator.gif)

##### Default use

```xml
<controls:AnimatedBusyIndicator IsActive="True"
                                BusyContent="I'm busy right now...">
    <controls:AnimatedBusyIndicator.AnimationContent>
        <lottie:LottieVisualSource UriSource="ms-appx:///Assets/LottieFiles/AlienIdScan.json" />
    </controls:AnimatedBusyIndicator.AnimationContent>
</controls:AnimatedBusyIndicator>
```

##### Useful customizable properties

```xml
<controls:AnimatedBusyIndicator IsActive="True"
                                BusyContent="Overriding default values..."
                                AnimationWidth="100"
                                AnimationHeight="100"
                                AnimationHorizontalAlignment="Center"
                                AnimationVerticalAlignment="Center">
    <controls:AnimatedBusyIndicator.AnimationContent>
        <lottie:LottieVisualSource UriSource="ms-appx:///Assets/LottieFiles/AlienIdScan.json" />
    </controls:AnimatedBusyIndicator.AnimationContent>
</controls:AnimatedBusyIndicator>
```

##### Custom content
```xml
<controls:AnimatedBusyIndicator IsActive="True">
    <controls:AnimatedBusyIndicator.BusyContent>
        <!-- The internal ContentPresenter will faithfully display your content, but can still take advantage of inherited properties like Foreground -->
        <TextBlock Text="I'm custom content, yay!" FontWeight="Bold" />
    </controls:AnimatedBusyIndicator.BusyContent>
    <controls:AnimatedBusyIndicator.AnimationContent>
        <lottie:LottieVisualSource UriSource="ms-appx:///Assets/LottieFiles/ChartLoading.json" />
    </controls:AnimatedBusyIndicator.AnimationContent>
</controls:AnimatedBusyIndicator>
```

##### 100% Templateable
```xml
<controls:AnimatedBusyIndicator>
    <controls:AnimatedBusyIndicator.Style>
        <Style TargetType="myControls:AnimatedBusyIndicator">
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate>
                        <Grid>
                            <Grid.Resources>
                                <animations:AnimationCollection x:Key="CommonShowAnimations">
                                    <animations:ScaleAnimation From="0.1"
                                                               To="1"
                                                               Delay="0:0:0.4"
                                                               Duration="0:0:0.8"
                                                               SetInitialValueBeforeDelay="True" />
                                    <animations:OpacityAnimation From="0"
                                                                 To="1"
                                                                 Delay="0:0:0.4"
                                                                 Duration="0:0:0.8"
                                                                 SetInitialValueBeforeDelay="True" />
                                </animations:AnimationCollection>
                                <animations:AnimationCollection x:Key="CommonHideAnimations">
                                    <animations:ScaleAnimation From="1"
                                                               To="0.1"
                                                               Duration="0:0:1.0" />
                                    <animations:OpacityAnimation From="1"
                                                                 To="0"
                                                                 Duration="0:0:1.0" />
                                </animations:AnimationCollection>
                            </Grid.Resources>

                            <StackPanel HorizontalAlignment="{TemplateBinding AnimationHorizontalAlignment}"
                                        VerticalAlignment="{TemplateBinding AnimationVerticalAlignment}">
                                <controls:AnimatedVisualPlayer x:Name="PART_Indicator"
                                                               AutoPlay="True"
                                                               Source="{TemplateBinding AnimationContent}"
                                                               Width="{TemplateBinding AnimationWidth}"
                                                               Height="{TemplateBinding AnimationHeight}"
                                                               extensions:VisualExtensions.NormalizedCenterPoint="0.5,0.5,0"
                                                               animations:Implicit.HideAnimations="{StaticResource CommonHideAnimations}"
                                                               animations:Implicit.ShowAnimations="{StaticResource CommonShowAnimations}"
                                                               Margin="10,10,10,5" />

                                <ContentPresenter x:Name="PART_BusyContentPresenter"
                                                  Content="{TemplateBinding BusyContent}"
                                                  Foreground="{TemplateBinding Foreground}"
                                                  Margin="0,5,0,10"
                                                  HorizontalAlignment="Center"
                                                  extensions:VisualExtensions.NormalizedCenterPoint="0.5,0.5,0"
                                                  animations:Implicit.HideAnimations="{StaticResource CommonHideAnimations}"
                                                  animations:Implicit.ShowAnimations="{StaticResource CommonShowAnimations}" />
                            </StackPanel>
                        </Grid>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>
    </controls:AnimatedBusyIndicator.Style>
</controls:AnimatedBusyIndicator>
```
