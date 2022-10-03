# 코드 리뷰 표준


코드 리뷰는 시간이 지남에 따라서 구글에서 작성된 코드 베이스의 상태를 우수한 상태로 유지하고 관리하는 것이 가장 주된 목적이다.
코드 리뷰의 모든 도구와 절차들은 이를 이루기 위해서 설계되었다.

이를 완수하기 위해서, 많은 곳에서 적절한 균형을 맞추어야 한다.

우선, 개발자는 본인 작업에 대해서 _make progress_ 가 가능해야 한다. (진전이 있음을 보여야 한다는 의미로 추측됨) 만약 코드 베이스에 어떤 개선 사항도 제출하지 못한다면, 코드 베이스는 절대로 개선될 수 없다. 또한 만약 리뷰어가 _any_ change (어떤 변화) 가 추가되게 어렵게 한다면, 개발자는 개선하는 작업에 대해서 동기부여가 안될 것이다.

이와 반대로, 리뷰어는 각각 CL(변화 목록)에 대해서 퀄리티를 검증할 책임이 있고, 이를 통해서, 시간이 흘러가도 코드 베이스의 전반적인 상태가 안좋게 변하는 것을 막아야 한다.
이것은 매우 어려울 수 있다. 왜냐하면, 코드베이스의 상태가 안좋게 되는 것은 시간이 지남에 따라 아주 조금씩 조금씩 안좋게 되는 것의 축적의 산물이기 때문이다. 특히 개발 팀이 시간에 심각하게 쫓기고 있고, 또 그들이 그 문제를 해결하기 위해서, (코드 품질을 저하시킴에도) 보다 편리한 지름길을 통해서 해결하고 할 수 있기 때문이다.

또한, 리뷰어들은 그들이 리뷰하는 코드에 대해서 주인의식과 책임감을 가져야 한다. 그들은 코드 베이스가 한결같고, 유지가능한 상태로 유지하는 것뿐 아니라 ["코드 리뷰의 목적은 무엇인가"](looking-for.md) 에서 언급한 모든 것에 대해 확실하게 책임을 져야 한다.

따라서, 우리는, 코드 리뷰에서 우리가 예상하는 표준 적인 룰을 아래와 같이 정했다.

**일반적으로, 리뷰어들은 CL이 반영된 상태에서 코드 베이스의 전체적인 상태가 개선되고, 모든 기능이 정상적으로 동작할 때만, 승인을 해여야 한다. 그것이 아니라면 CL은 불완전한 상태이기 때문에 리뷰어는 승인을 하면 안된다.

이것은 모든 코드 리뷰 가이드 라인의 _가장_ 중요하고 우선적인 전제이고 규칙이다. 

물론 이것에도 한계는 있다. 예를 들어, 만약 리뷰어가 그들의 시스템에 추가되기를 원하지 않는 기능이 CL로 추가되었을 때, CL이 잘 디자인 되어있더라도, 리뷰어가 이것을 코드베이스에 반영하는 것을 막을 수 있는 점이다.

여기서 중요한 점은, "완벽한" 코드가 아닌,
A key point here is that there is no such thing as "perfect" code&mdash;there is
only _better_ code. Reviewers should not require the author to polish every tiny
piece of a CL before granting approval. Rather, the reviewer should balance out
the need to make forward progress compared to the importance of the changes they
are suggesting. Instead of seeking perfection, what a reviewer should seek is
_continuous improvement_. A CL that, as a whole, improves the maintainability,
readability, and understandability of the system shouldn't be delayed for days
or weeks because it isn't "perfect."

Reviewers should _always_ feel free to leave comments expressing that something
could be better, but if it's not very important, prefix it with something like
"Nit: " to let the author know that it's just a point of polish that they could
choose to ignore.

Note: Nothing in this document justifies checking in CLs that definitely
_worsen_ the overall code health of the system. The only time you would do that
would be in an [emergency](../emergencies.md).

## Mentoring

Code review can have an important function of teaching developers something new
about a language, a framework, or general software design principles. It's
always fine to leave comments that help a developer learn something new. Sharing
knowledge is part of improving the code health of a system over time. Just keep
in mind that if your comment is purely educational, but not critical to meeting
the standards described in this document, prefix it with "Nit: " or otherwise
indicate that it's not mandatory for the author to resolve it in this CL.

## Principles {#principles}

*   Technical facts and data overrule opinions and personal preferences.

*   On matters of style, the [style guide](http://google.github.io/styleguide/)
    is the absolute authority. Any purely style point (whitespace, etc.) that is
    not in the style guide is a matter of personal preference. The style should
    be consistent with what is there. If there is no previous style, accept the
    author's.

*   **Aspects of software design are almost never a pure style issue or just a
    personal preference.** They are based on underlying principles and should be
    weighed on those principles, not simply by personal opinion. Sometimes there
    are a few valid options. If the author can demonstrate (either through data
    or based on solid engineering principles) that several approaches are
    equally valid, then the reviewer should accept the preference of the author.
    Otherwise the choice is dictated by standard principles of software design.

*   If no other rule applies, then the reviewer may ask the author to be
    consistent with what is in the current codebase, as long as that doesn't
    worsen the overall code health of the system.

## Resolving Conflicts {#conflicts}

In any conflict on a code review, the first step should always be for the
developer and reviewer to try to come to consensus, based on the contents of
this document and the other documents in
[The CL Author's Guide](../developer/index.md) and this
[Reviewer Guide](index.md).

When coming to consensus becomes especially difficult, it can help to have a
face-to-face meeting or a video conference between the reviewer and the author, instead of
just trying to resolve the conflict through code review comments. (If you do
this, though, make sure to record the results of the discussion as a comment on
the CL, for future readers.)

If that doesn't resolve the situation, the most common way to resolve it would
be to escalate. Often the
escalation path is to a broader team discussion, having a Technical Lead weigh in, asking
for a decision from a maintainer of the code, or asking an Eng Manager to help
out. **Don't let a CL sit around because the author and the reviewer can't come
to an agreement.**

Next: [What to look for in a code review](looking-for.md)
