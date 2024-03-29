A Node.js wrapper for Apple's [EventKit](https://developer.apple.com/documentation/eventkit) framework. **Note: only supports macOS**


### ~~Features~~ - coming soon

### ~~Usage~~ -  coming soon

```typescript
```

---

### Todo

- roadmap
	- NSPredicate provide calendar
	-  EKEvent implement IAdaptable
	- cdecl Event(withIdentifier: string)

notes:
_cdecl_ refers to [this](https://forums.swift.org/t/formalizing-cdecl/40677/11) undocumented swift attribute

- _native_ package (contains swift files that compile to dynamic libraries. these dynamic libraries contain exported symbols which are used for interfacing)
	-  EventStore.swift
		- [x] implement init()
			- https://developer.apple.com/documentation/eventkit/ekeventstore/1507252-init
		- [x] implement cdecl init(sources: [EKSources]) 
			-  https://developer.apple.com/documentation/eventkit/ekeventstore/1507179-init
		- [x] implement cdecl freePointer 
		- [x] implement cdecl sources() 
			-  https://developer.apple.com/documentation/eventkit/ekeventstore/1507315-sources
		- [x] implement cdecl calendars(for: EKEntityType)
			- https://developer.apple.com/documentation/eventkit/ekeventstore/1507128-calendars
		- [ ] ~~implement predicateForEvents(startDate: Date, endDate: Date, calendars: [EKCalendars])~~
			-  https://developer.apple.com/documentation/eventkit/ekeventstore/1507479-predicateforevents
		- [ ] ~~implement cdecl requestAccess function~~
		- [x] implement cdecl events(matching: predicate) 
			-  https://developer.apple.com/documentation/eventkit/ekeventstore/1507183-events
		- [ ] #1 implement cdecl event(withIdentifier: String)
	- models
		- [x] use codable protocol on models to enable serialisation
		- [x] define EKCalendarModel 
			- [x] implement toBuiltin method
			- [x] implement init from builtin type
		- [x] define EKSourceModel
			- [x] implement init from builtin type
			- [x] implement toBuiltin method
		- [x] define EKEventModel
			- [ ] implement toBuiltin method
			- [x] implement init from builtin type
		- [x] define NSPredicateModel
		- [x] define CGColorModel
			- [x] implement init from builtin
			- [x] ~~implement conversion of CGColor components property to rgb~~
		      
- _EventKitJS_ wrapper
	- [x] implement darwin os check
	- [x] implement static getter exposing EventStore
	- [x] implement static method to check calendar/reminder permissions
	- EventStore class
		- [x] implement constructor for both default EKEventStore() instantiation and EKEventStore(sources: [EKSources]) instantiation with sources argument
		- [x] implement sources() method
		- [x] implement calendars(for: EKEntityType) method
		- [x] implement predicateForEvents(startDate: Date, endDate: Date, calendars: [EKCalendars])
		- [x] implement events(matching: NSPredicate) method
        - [ ] #1 implement event(withIdentifier identifier: String) method
	 - models
		 - [x] define a model that represents calendar/reminder permission status
		 - [x] define CStringPointer
		 - [x] define EKCalendar
			 - [ ] implement IAdaptable
		 - [x] define EKCalendarType
			 - [x] implement IAdaptable
		 - [x] define CGColor
			 - [ ] implement IAdaptable
		 - [x] define EKSource
			- [ ] implement IAdaptable
		 - [x] define EKEntityMask.ts
			- [x] implement IAdaptable
		 - [x] define EKEvent
			- [ ] implement IAdaptable
			- [x] extend from EKCalendarItem
		 - [x] define abstract EKCalendarItem
		 - [x] define NSPredicate
			- [ ] implement IAdaptable
		 - [x] define EKEntityType
			- [ ] implement IAdaptable
		- [x] define EKSourceType
			- [x] implement IAdaptable
	- interfaces
		- IAdaptable.ts (for implementing two way conversions between swift types and nodejs types) - each model is responsible for implementing conversion upon their primitive unique fields
			- [x] define fromSwiftModel(object: any): any
			- [x] define toSwiftModel(): any
	-  adapters
		-  ModelsAdapter.ts
			- [x] implement static function adaptModelToSwift()
				- takes model instance as argument, or an array of said model instances
				- returns resulting new object or array of objects with toSwiftModel applied
			- [x] implement static function adaptModelFromSwift()
				- takes new instance of T or [T] as model argument
				- takes any object or [any object] as object argument
				- returns instance of T or [T] with fromSwiftModel applied
	-  DateAdapter.ts
		- NOTE: default encoding of swift date model to json is ms since 2001/1/1
		- [x] implement static function toSwiftDate(date: Date)
		- [x] implement static function fromSwiftDate(date: number)
- Other
	- [ ] abstract the dynamic library build process (for the sake of usability).. maybe prebuild and distribute binaries?
	- [ ] setup packaging and publish to npm
	      
	      


