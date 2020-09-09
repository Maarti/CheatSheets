
# Angular Testing cheatsheet

## [Testing asynchronous code](https://angular.io/guide/testing#async-test-with-async)
To test components with promises, setTimeout(),... wrap the test spec function in a `async` function and execute the tests when the `whenStable` promise resolves.
```typescript
    it('should refresh the paginator', async(() => {
      const calculationsLength = component.calculations.length;
      expect(component.paginator.length).toBe(calculationsLength);
      component.calculations.splice(0, 1);
      component.refreshData();
      fixture.whenStable().then(() => {
        fixture.detectChanges();
        expect(component.paginator.length).toBe(calculationsLength - 1);
      });
    }));
```
 `fixture.whenStable()` resolves when the JavaScript engine's task queue becomes empty.

## Testing output events and button click
`spyOn` the emit method of the EventEmitter and call `click()` on the the button
```typescript
    it('should emit executeAgain event on click on the "Execute Again" button', async () => {
      spyOn(component.executeAgain, 'emit');
      const button = fixture.nativeElement.querySelector('.mat-icon-button');
      button.click();
      const executeAgainButton = fixture.nativeElement.parentNode.querySelector('.mat-menu-panel #menuItem0');
      expect(component.executeAgain.emit).not.toHaveBeenCalled();
      executeAgainButton.click();
      expect(component.executeAgain.emit).toHaveBeenCalled();
    });
```

### Spy on private function
```
spyOn<any>(component, 'handleSubscribe');
expect(component['handleSubscribe']).not.toHaveBeenCalled();
```

## Declare Entry Components when testing
When a component must be declared in `entryComponents` (for example, to test a MatDialog):
```typescript
  beforeEach(async(() => {
    TestBed.configureTestingModule({
      imports: [
         MatDialogModule,
         NoopAnimationsModule,      
      ],
      providers: [
        { provide: MatDialogRef, useValue: mockDialogRef },
        {
          provide: MAT_DIALOG_DATA,
          useValue: { 
            metadata: MetadataMock,
            calculations: CalculationMock,
            isError: false,
          }
        }
      ],
      schemas: [CUSTOM_ELEMENTS_SCHEMA],
      declarations: [MyDialogComponent]
    });

    TestBed.overrideModule(BrowserDynamicTestingModule, {
      set: {
        entryComponents: [MyDialogComponent]
      }
    });

    TestBed.compileComponents();
  }));
```

## Expecting value inside a subscribe
Add the `done()` parameter and call it at the end of the `subscribe()`
```
it("should fail", (done) => {
    // ...
    obs.subscribe((value) => {        
        expect(true).toBe(false);
        done();
    });
});
```
Or [return a promise](https://github.com/jest-community/eslint-plugin-jest/issues/494#issuecomment-562094733)
```
it("should fail", () => {
    // ...
    return new Promise(resolve => {
	    obs.subscribe((value) => {        
           expect(true).toBe(false);
           resolve();
        });
    });
});
```

## NGRX
### Testing side effect of an Effect
Important part: the `actions$` must be a `of()` and not a `hot()` to resolve instantly
```
it('should call the getData() method', () => {
  actions$ = of(action());
  service.getData = jest.fn();
  effects.loadData$.subscribe();
  expect(service.getData).toHaveBeenCalledWith('id');
});
```


## Resources
* [Angular Testing Guide](https://angular.io/guide/testing)
* [Angular Cheatsheet](https://angular.io/guide/cheatsheet)
* [Angular Test Driven Development Guide](https://angularfirebase.com/lessons/angular-testing-guide-including-firebase/)
