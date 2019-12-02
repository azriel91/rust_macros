# 👥 Reduce duplication

**Scenario:** Writing similar syntax.

<details open>

<summary>Without macro</summary>

```rust,ignore
#[test]
fn on_start_delegates_to_state() {
    let (mut state, mut world, invocations): (RobotState<(), ()>, _, _) =
        setup_without_intercepts();

    state.on_start(StateData::new(&mut world, &mut ()));

    assert_eq!(vec![Invocation::OnStart], *invocations.borrow());
}

#[test]
fn on_stop_delegates_to_state() {
    let (mut state, mut world, invocations): (RobotState<(), ()>, _, _) =
        setup_without_intercepts();

    state.on_stop(StateData::new(&mut world, &mut ()));

    assert_eq!(vec![Invocation::OnStop], *invocations.borrow());
}

#[test]
fn on_pause_delegates_to_state() {
    let (mut state, mut world, invocations): (RobotState<(), ()>, _, _) =
        setup_without_intercepts();

    state.on_pause(StateData::new(&mut world, &mut ()));

    assert_eq!(vec![Invocation::OnPause], *invocations.borrow());
}

// ..
```

</details>

<details open>

<summary>With macro</summary>

```rust,ignore
#[macro_use]
macro_rules! delegate_test {
    ($test_name:ident, $function:ident, $invocation:expr) => {
        #[test]
        fn $test_name() {
            let (mut state, mut world, invocations): (RobotState<(), ()>, _, _) =
                setup_without_intercepts();

            state.$function(StateData::new(&mut world, &mut ()));

            assert_eq!(vec![$invocation], *invocations.borrow());
        }
    };
}

delegate_test!(on_start_delegates_to_state, on_start, Invocation::OnStart);
delegate_test!(on_stop_delegates_to_state, on_stop, Invocation::OnStop);
delegate_test!(on_pause_delegates_to_state, on_pause, Invocation::OnPause);
// ..
```

</details>
