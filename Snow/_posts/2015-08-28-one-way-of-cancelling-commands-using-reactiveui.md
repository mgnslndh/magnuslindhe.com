---
layout: post
tags: ReactiveUI
categories: ReactiveUI
title: One way of cancelling commands using ReactiveUI
---

I was looking for a way to cancel a `ReactiveCommand<T>` in [ReactiveUI](http://reactiveui.net/ "ReactiveUI website") but could not find any good official documentation on this. Instead I came up on [Gluck's solution on StackOverflow](http://stackoverflow.com/a/31636333/966) (surprise!).
<!--excerpt-->
This is one way you can cancel a command using ReactiveUI 6:

	public class ThisViewModelCanCancelCommands
	{
		public ReactiveCommand<Unit> Poll { get; private set; }
		public ReactiveCommand<object> Cancel { get; private set; }
		private IPoller poller = new Poller(); // Dummy service for example;
		
		public ThisViewModelCanCancelCommands()
		{
			Poll = ReactiveCommand.CreateAsyncObservable<Unit>(
					this.WhenAnyObservable(vm => vm.Poll.IsExecuting).Select(v => v == false), // In order to disable button when executing
					_ => Observable.StartAsync(PollHandler).TakeUntil(Cancel)
					);
	
			Cancel = this.WhenAnyObservable(vm => vm.Poll.IsExecuting).ToCommand();
		}
		
		private Task PollHandler(CancellationToken ct)
		{
			return poller.RunAsync(ct);
		}
	}


