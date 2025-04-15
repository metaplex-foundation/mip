<h1>Procedure for Metaplex Improvement Proposals (“MIPs”) for the Metaplex Program Library</h1>

**TDLR: The Metaplex Foundation will implement the following procedure for MIPs for: (1) Token Metadata before it is made immutable; and (2) for the rest of the Metaplex Program Library on an ongoing basis:**
1. **Proposals.** Anyone may propose a MIP by: (1) proving ownership of 200 $MPLX; and (2) paying 10 USDC as a means to reduce spam (the Metaplex Foundation will refund the USDC for submissions made in good faith).
2. **Community Feedback Period & Initial Review.** The community will be able to provide feedback on proposed MIPs on the Metaplex Foundation Github Repo. 
    * During the community feedback period, the Metaplex Foundation will screen out spam, proposals that lack critical details, and those that would violate the following hard requirements:
        * No unnecessary breaking of any backwards compatibility 
        * Nothing that compromises the security of user assets and metadata (e.g., modifying metadata on specific tokens)
        * Compliance with all applicable laws and regulations 
    * In addition, the Metaplex Foundation will screen out proposed MIPs for Token Metadata or Bubblegum that would violate any of these additional hard requirements: 
        * No token-gating with $MPLX for accessing the functionality of Token Metadata or Bubblegum
        * Equal access for all callers to the functionality of Token Metadata or Bubblegum
        * Equal application of instruction level fees
        * No requirement for new NFT collections to be tradeable on an open liquidity layer if an open liquidity layer is built
        * No hindering the ability to achieve the timeline for rendering Token Metadata immutable 
3. **Implementation Designation.** At the end of the community feedback period, the Metaplex Foundation will designate whether the proposed MIP – if passed – will be implemented by the Foundation itself or whether the community will be called upon to implement it. 
4. **Voting Period.** Following the community feedback period, the Metaplex Foundation will open the voting period. Voting will be based on MPLX ownership, meaning that one MPLX equals one vote. The Metaplex Foundation will specify the minimum number of total votes that must be submitted for the vote to count. Approval requires (a) >66% of votes are “Yes” votes, and (b) total votes cast exceeds the specified minimum number of votes.
5. **MIP Implementation.**
    * Foundation Implementation. If the approved MIP was designated for Foundation implementation, the Metaplex Foundation will publish a development timeline and then exercise reasonable efforts to achieve its proposed timeline. Core software development will be done in public in source available repos, as is currently the case. 
    * Community Implementation. If the approved MIP was designated for Community implementation, the Metaplex Foundation will request bids from the community for implementation. 
        * The Metaplex Foundation will review all bids and select a winning bid.
        * The winning bid must enter into a customary legal contract for the scope of work and must follow customary procedures for submitting pull requests, reviewing pull requests, following code standards, running tests, and public review.
    * Audits. The Metaplex Foundation will facilitate security audits with third party auditors on all significant changes to the Token Metadata program.
6. **Metaplex Updates.** While the Metaplex Foundation will endeavor to propose changes to the Metaplex Program Library through the MIP process, the Metaplex Foundation may make changes without going through the above defined process, provided that the Metaplex Foundation does not make changes that are inconsistent with an approved MIP or that would violate hard requirements. As is already the case, every change the Metaplex Foundation makes to the Metaplex Program Library will be available in the repo and open to community comment.

<h2>Full Procedure for MIPs for the Metaplex Program Library</h2>

This procedure will apply to proposed changes to: (1) Token Metadata before update authority for Token Metadata is transferred to security firms and it is made immutable; and (2) the rest of the Metaplex Program Library on an ongoing basis. 

The Metaplex Program Library includes the programs found here: \
(https://developers.metaplex.com/programs-and-tools)

The Metaplex Foundation’s goal with this procedure is to provide a workable framework for community contribution and governance for the Metaplex Program Library. Community governance is a fairly new concept that is both difficult and ripe for experimentation. We expect to learn as we go and to make adjustments based on both our observations and community feedback.  

We hope to receive community MIP submissions that would do some or all of the following:

* Provide technical improvements that increase value to the community and grow usage.
* Increased efficiency that improves cost and performance.
* Address specific needs voiced by the community of app developers, creators and collectors that rely on the programs.
* Further the principles of permission-lessness, censorship resistance, or decentralization.

<h2>Proposals</h2>

Any MPLX holder (the “Original Proposer”) may propose a “Community MIP”  to the Metaplex source available code repository (currently Github, located here: ([https://github.com/metaplex-foundation/mip/](https://github.com/metaplex-foundation/mip/)) (the “Repo”) by (1) proving ownership of 200 $MPLX (subject to revision by Metaplex Foundation based on the market price of MPLX); and (2) paying 10 USDC on the Metaplex governance website, located here: (https://mip.metaplex.com). 

If a Community MIP submission is legitimate (i.e., not spam, not made in bad faith) then Metaplex Foundation will refund the 10 USDC payment to the Original Proposer. The reason we are requiring a 10 USDC payment for each submission is to prevent being spammed. We expect to receive a large number of submissions and are committing to review all of them. We are open to changing the submission requirements to find the right balance to prevent spam but also not discourage legitimate submissions. 

The process for proposing Community MIPs may evolve over time as we learn from our experience and community feedback. 

<h2>Community Feedback & Initial Review</h2>

Each Community MIP proposal will trigger a 14 day “Community Feedback Period”, during which anyone may comment on the Community MIP in the Repo. This will provide time for the community to voice its opinion on each Community MIP before a DAO vote is held. We encourage Original Proposers to indicate in the comments whether they are ready, willing and able to implement the proposed MIP themselves.

During the Community Feedback Period, the Metaplex Foundation will review the Community MIP to screen out ones that are spam, made in bad faith, lack critical details, or would violate any of the following hard requirements (collectively, “Hard Requirements”):

* No unnecessary breaking of any backwards compatibility 
* Nothing that compromises the security of user assets and metadata (e.g., modifying metadata on specific tokens)
* Compliance with all applicable laws and regulations

In addition, the Metaplex Foundation will screen out proposed MIPs for Token Metadata or Bubblegum that would violate any of these additional hard requirements (collectively, “Additional Hard Requirements”): 

* No token-gating with $MPLX for accessing the functionality of Token Metadata or Bubblegum
* Equal access for all callers to the functionality of Token Metadata or Bubblegum
* Equal application of instruction level fees
* No requirement for new NFT collections to be tradeable on an open liquidity layer if an open liquidity layer is built
* No hindering the ability to achieve the timeline for rendering Token Metadata immutable 

The Metaplex Foundation’s goal is to complete an initial screening decision for each Community MIP within 7 days of publication on the Repo. If we are unable to meet that goal for any particular submission, we will publish an update on the Repo with a new target date for our decision. If a Community MIP is not screened out as spam or for being made in bad faith, the Metaplex Foundation will refund the 10 USDC submission payment to the Original Proposer. 

If the Metaplex Foundation screens out a Community MIP it will post the rationale for doing so on the Repo. Community MIPs that are screened out will be removed from consideration. 

The Original Proposer may withdraw the Community MIP at any time prior to the end of the Community Feedback Period (the Metaplex Foundation will refund the 10 USDC for submissions made in good faith).

<h2>Implementation Designation</h2>

At the end of the 14-day Community Feedback Period, a Community MIP will convert to an officially numbered MIP (e.g., MIP-72), unless it has been screened out. 

For each officially numbered MIP, the Metaplex Foundation will designate whether the MIP – if passed – will be implemented by the Foundation itself (“Foundation Implementation Designation”) or whether the community will be called upon to implement it (“Community Implementation Designation”). 

This decision will be based largely on whether the Metaplex Foundation has the ability to timely perform the implementation itself. However, if that is not possible, the Metaplex Foundation will call upon the community to implement the MIP if it passes the DAO vote. 

<h2>Voting Period</h2>

Within 7 days after the Community Feedback Period closes for a MIP, the Metaplex Foundation will publish finalized language for the MIP based upon the Community MIP submission. This will include whether the MIP received a Foundation or Community Implementation Designation. The Metaplex Foundation will then open the “Voting Period” which shall remain open for 14 days.  

When the Metaplex Foundation opens the Voting Period, it will specify the minimum number of total votes that must be submitted for the vote to count (the “Voting Threshold”).  Voting will be based on MPLX ownership, meaning that one MPLX equals one vote. The Metaplex Foundation will announce via Twitter (@MetaplexFndn) and on the Metaplex Discord channel when a Voting Period is beginning and direct the community to where it can cast votes on the Metaplex DAO. The voting mechanics may change in the future as we learn from experience.

Once the Voting Period closes, the MIP will either pass and convert to an “Approved MIP,” or will fail and convert to a “Rejected MIP.”  The MIP will pass and convert to an Approved MIP if (a) >66% of votes are “Yes” votes, and (b) total votes cast exceed the Voting Threshold.  If either condition is not met, the MIP shall fail and convert to a Rejected MIP.  

<h2>Foundation Implementation</h2>

If an Approved MIP carries a Foundation Implementation Designation, then the Metaplex Foundation will aim to publish a proposed development timeline within 14 days. If the Metaplex Foundation is unable to meet that target deadline, it will publish its rationale for extending the target deadline and in doing so will set a new deadline by which it will publish the development timeline. Each development timeline will specify that an independent security audit (coordinated by the Metaplex Foundation) will occur and the timeline for such audit. Once the development timeline is published, the Metaplex Foundation will then exercise reasonable efforts to achieve its proposed timeline. The Metaplex Foundation’s work implementing any MIPs will be done publicly in the Repo and open to community comment.

<h2>Community Implementation</h2> 

If an Approved MIP carries a Community Implementation Designation, then the following shall occur (together, the “Community Implementation Procedure”):

The Metaplex Foundation shall enact a bidding process within 7 days which shall define the scope outlined in the Approved MIP. The bidding process is designed to ensure we delegate the implementation to community members with the best proposal and with the requisite technical capabilities to implement it.  

For a period of 14 days (the “Bidding Period”), the Metaplex Foundation will accept and evaluate bids, but only those which comply with all of the following requirements:

* The bid must specify the requested compensation;
* The bid must include a technical design proposal;
* The bid must include a timeline for pull requests/code submission; and
* The bid must be publicly submitted on the Repo.

The Metaplex Foundation will review all compliant bids and, within 7 days after the Bidding Period closes, will publish its selection of the best bid (the “Winning Bid”), based on the following non-exhaustive list of criteria:

* Whether and the extent to which the bid fulfills the requirements of the Approved MIP;
* The strength of the proposed technical design;
* The proposed cost structure; and
* The proposed timeline.

However, if the Metaplex Foundation finds none of the bids to be satisfactory, it may reject all bids which will result in an extension of the Bidding Period to accept new bids.

To accept the offer to implement the Approved MIP, the Winning Bidder must enter into a customary legal contract for the scope of work with the Metaplex Foundation that will govern the services provided (the “Governing Documentation”).

After the Winning Bid is selected and the Governing Documentation is executed, the Winning Bidder will follow customary procedures for submitting pull requests, reviewing pull requests, following code standards, running tests, and public review. This will all be done in public and available for community comment in the Repo. 

Once the pull request is in a code complete state, the Metaplex Foundation will coordinate an independent security audit.  

Once all security issues identified are fixed, all comments and change requests have been resolved, and all contribution guidelines have been met, the Metaplex Foundation will merge the new code and schedule deployment. 

The Metaplex Foundation may allow extensions to the timeline in its sole discretion, consistent with the Governing Documentation.

The Metaplex Foundation shall model industry best practices for deploying the Metaplex Program Library using automated processes where reasonably possible. Notification cadence and “baking time” in Devnet will depend on the type of the release (major, minor or patch).

<h2>Metaplex Changes to Metaplex Program Library</h2>

While the Metaplex Foundation will endeavor to propose changes to the Metaplex Program Library through the above defined process, the Metaplex Foundation may make changes without going through the above defined process, provided that the Metaplex Foundation does not make changes that are inconsistent with an Approved MIP.  The Metaplex Foundation will never make a change that fails to comply with: (1) any of the Hard Requirements for all of the Metaplex Program Library; and (2) any of the Additional Hard Requirements for Token Metadata or Bubblegum.

We are committed to building in public. As is already the case, every change the Metaplex Foundation makes to the Metaplex Program Library will be available in the Repo and open to community comment. We will regularly update the community on Twitter and in the Metaplex Discord channel. 

**<span style="text-decoration:underline;">Disclaimer</span>.** The Metaplex Foundation may terminate a MIP at any point in the process if it comes into conflict with applicable laws or regulations. 

<h2>FAQs</h2>

1. Who may issue a MIP?

Any MPLX holder may propose a Community MIP.  

2. What means of input does the Solana Community have on the MIP process?

The Solana Community has multiple levels of input on the MIP process.  First, any MPLX holder may submit a Community MIP.  Second, anyone may comment on any Community MIP during the Community Feedback Period.  Third, any MPLX holder may vote on a MIP.  Fourth, anyone may submit a bid to implement an Approved MIP if a Community Implementation Designation occurs.

3. What means of communication are used for the MIP process?

Community MIPs may be viewed and discussed on the Repo. Decisions from the Metaplex Foundation in screening out Community MIPs will be published on the Repo and available for public comment. The Metaplex Foundation shall notify the community via a tweet from official Metaplex accounts and in the Metaplex Discord of any of the following events occurring, promptly after such event occurs: (a) a Voting Period begins, (b) a Voting Period ends (which tweet or series of tweets shall include the results of the vote), (c) a Voting Period is extended, and, in the event of a Community Implementation, (d) the opening of a Bidding Period, (e) the selection of a Winning Bid, or (f) the extension of a Bidding Period. Furthermore, the Metaplex Foundation will regularly provide updates on the progress for MIP implementation. All changes to Token Metadata and the Metaplex Program Library will be made available in the Repo and open to community comment.

4. What parameters constitute acceptance or rejection of a MIP?

MIPs shall pass and convert to an Approved MIP if (a) >66% of votes are “Yes” votes, and (b) total votes exceed the Voting Threshold.  A MIP shall fail and convert to a Rejected MIP under all other circumstances.

5. How is “rough consensus” documented within proposals after they have been made available for public comment?

A summary of the feedback from the “Community Feedback Period” will be added to the proposal after the 21-day period.

6. What is the development schedule for MIPs after they are approved? 

If a MIP is Approved with Foundation Implementation Designation, then the Metaplex Foundation shall publish a development timeline within 14 days, which shall include a determination of whether a security audit will be necessary and the timeline to do so.  The Metaplex Foundation may, in its discretion, extend the deadline to publish the proposed development timeline, but must publish its rationale for doing so as well as a new deadline by which it will publish such development timeline.  The Metaplex Foundation will then exercise reasonable efforts to achieve its proposed timeline.  If, on the other hand, a Community Deferral Decision occurs, then the Community Implementation Procedure will be followed.

7. Are there any meaningful differences in process depending on the type of topic or issue addressed by a MIP?

No - The process shall be the same for all potential topics covered by the MIP process. However, the criteria for screening out proposals is different for Token Metadata and Bubblegum than for the rest of the Metaplex Program Library. 
