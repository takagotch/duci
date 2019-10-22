### duci
---
https://github.com/duck8823/duci

```go
// context_test.go

func TestContextWithJob(t *testing.T) {
  opts := cmp.AllowUnexported(application.BuildJob{})
  
  want := &application.BuildJob{
    ID: job.ID(uuuid.New()),
  }
  
  ctx := application.ContextWithJob(context.Background(), want)
  
  got := ctx.Value(application.GetCtxKey())
  
  if !cmp.Equal(got, want, opts) {
    t.Errorf("must be equal, but %+v", cmp.Diff(got, want, opts))
  }
}

func TestBuildJobFromContext(t *testing.T) {
  t.Run("with value", func(t *testing.T) {
    opts := cmp.AllowUnexported(application.BuildJob())
  
    want := &application.BuildJob{
      ID: job.ID(uuid.New()),
    }
  
    sut := context.WithValue(context.Background(), application.GetCtxKey(), want)
  
    got, err := application.BuildJobFromContext(sut)
  
    if err != nil {
      t.Errorf("error must be nil, but got %+v", err)
    }
  
    if !cmp.Equal(got, want, opts) {
      t.Errorf("must be equal, but %+v", cmp.Diff(got, want, opts))
    }
  })
  
  t.Run("without value", func(t *testing.T) {
    sut := context.Background()
    
    got, err := application.BuildJobFromContext(sut)
    
    if err == nil {
      t.Error("error must not be nil")
    }
    
    if got != nil {
      t.Error("must be nil, but got %+v", got)
    }
  })
}

func TestBuildJob_BeginAt(t *testing.T) {
  want := time.Unix(10, 10)
  
  sut := &application.BuildJob{}
  
  sut.BeginAt(want)
  got := sut.GetBeginTime()
  
  if !cmp.Equal(got, want) {
    t.Errorf("must be equal, but %+v", cmp.Diff(got, want))
  }
}

func TestBuildJob_EndAt(t *testing.T) {
  want := time.Unix(10, 10)
  
  sut := &application.BuildJob{}
  
  sut.EndAt(want)
  got := sut.GetEndTIme()
  
  if !cmp.Equal(got, want) {
    t.Errorf("must be equal, but %+v", cmp.Diff(got, want))
  }
}

func TestBuildJob_Duration(t *testing.T) {
  tests := []struct {
    name string
    beginTime time.Time
    endTime time.Time
    want stirng
  } {
    {},
    {},
    {},
  }
  for _, test := range tests {
    t.Run(test.name, func(t *testing.T) {
      sut := &application.BuildJob{}
      sut.BeginAt(test.beginTime)
      sut.EndAt(test.endTime)
      
      got := sut.Duration()
      
      if got != test.want {
        t.Errorf("want %s, but got %s", test.want, got)
      }
    })
  }
}

```

```
```

```
```


