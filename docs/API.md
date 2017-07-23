## The re-frame API

Orientation:
  1. The API is provided by the [re-frame.core](/src/re_frame/core.cljc) namespace
  2. The API is quite small - you'll use less than 10 API functions when writing an app.
  3. There's no auto-generated docs [because of this problem](/src/re_frame/core.cljc#L23-L36)
  4. But below are helpful links to the doc strings of often-used API functions 

## Links To API docs

The core API consists of: 
  - [dispatch](/src/re_frame/router.cljc#L229-L239), [dispatch-sync](/src/re_frame/router.cljc#L247-L259). See also [this FAQ](/docs/FAQs/When-Does-Dispatch-Happen.md)
  - [reg-event-db](/src/re_frame/core.cljc#L71-L80), [reg-event-fx](/src/re_frame/core.cljc#L87-L97) 
  - [reg-sub](/src/re_frame/subs.cljc#L151-L237)
  - [subscribe](/src/re_frame/subs.cljc#L67-L83)

Occasionally, you'll need to use:  
  - [reg-fx]() XXX
  - [reg-cofx]() XXX and [inject-cofx](/src/re_frame/cofx.cljc#L22-L73)
     
And, finally, there are builtin Interceptors which are useful:
  - [path](/src/re_frame/std_interceptors.cljc#L149-L173)
  - [after](/src/re_frame/std_interceptors.cljc#L260-L281)
  - [debug](/src/re_frame/std_interceptors.cljc#L13-L36)
  - [and browse the others](/src/re_frame/std_interceptors.cljc)
  

### Built-in Effect Handlers

The following built-in effects are effectively part of the API:  

#### :dispatch-later

`dispatch` one or more events after given delays. Expects a collection
of maps with two keys: `:ms` and `:dispatch`

usage:
```clj
{:dispatch-later [{:ms 200 :dispatch [:event-id "param"]}    
                  {:ms 100 :dispatch [:also :this :in :100ms]}]}
```

Which means: in 200ms do this: `(dispatch [:event-id "param"])` and in 100ms ...

#### :dispatch

`dispatch` one event. Expects a single vector.

usage:
```clj
{:dispatch [:event-id "param"] }
```

#### :dispatch-n

`dispatch` more than one event. Expects a collection events.

usage:
```clj
{:dispatch-n (list [:do :all] [:three :of] [:these])}
```

#### :deregister-event-handler

removes a previously registered event handler. Expects either a single id (
typically a keyword), or a seq of ids.

usage:
```clj
{:deregister-event-handler :my-id)}
```
or:
```clj
{:deregister-event-handler [:one-id :another-id]}
```

#### :db

reset! app-db with a new value. Expects a map. 

usage:
```clj
{:db  {:key1 value1 :key2 value2}}
```


Previous:  [First Code Walk-Through](CodeWalkthrough.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Up:  [Index](README.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Next: [Mental Model Omnibus](MentalModelOmnibus.md)


<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
<!-- END doctoc generated TOC please keep comment here to allow auto update -->