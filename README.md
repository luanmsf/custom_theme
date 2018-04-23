# custom_theme

The ideal is based on LayoutInflater and ViewRoot of an Activity.

To more specific detail, We have two cases for changing Theme:
 + App runs at first time, Using a customised LayoutInflater to catch views created (ThemeLayoutInflater) then create ViewAware instance that
 is compatible with View class of view instance created from customised LayoutInflater (ViewAwareTable & ThemeWrapper), 
 the ViewAware will store on compatible view instance(setTag) for next using and end step is applying theme using.
 
    Simple flow:
 
   (Activity)onCreate -> (ThemeWrapper)init{store ActivityAware into RootView} -> (Factory&Factory2)createView -> (InflaterObserver)onViewCreated->[(ViewAwareTable)findViewAwareClass -> (ThemeWrapper)instanceAware -> storeViewAwareInstance -> applyTheme] 
 
 + App is running, user makes a change theme, get rootview from ActivityAware, has been stored before, explain sub view from rootview to find approriate viewAware to apply new theme on its attr
 
   Simple flow:
   
   (ThemeWrapper)applyTheme(theme){call from user's action} -> (ThemeActivity)onThemeChanged -> (ThemeWrapper)applyTheme(activity,theme) -> (ActivityHolder)notifyThemeChanged -> (ActivityAware)onThemeChanged -> (ThemeWrapper)applyTheme(view,theme) ->[find viewAware of view and apply theme]
 
 + Note:
      +(xxx)yyy : xxx= class, yyy = method inside the class
      +{abc}:   explaining words
      +[]:    block of complicated action
